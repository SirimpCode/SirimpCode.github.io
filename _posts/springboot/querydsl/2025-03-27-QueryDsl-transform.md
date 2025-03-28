---
title: "QueryDSL transform 활용 하여 그룹화"
date: 2025-03-27 09:42:31 +0900
categories: [Spring Boot, QueryDSL]
tags: [Java, Spring Boot, QueryDSL, for, 반복문]
math: true
toc: true # 패널 목차
#만약 너가 이 기능을 끄고싶다면 _config.yml파일로가서 toc값을 false로 바꾸어주면된다. 
pin: true
img_path: /assets/img/javaandeclipse/
image:
  path: /assets/img/thumbnail/querydsl.png
#  alt: 이클립스와 자바
---

## 작성한 쿼리문

> **QueryDSL를 이용한 참여 목록 조회 메서드 설명**  
> 해당 메서드는 **Competition ID**를 기준으로 참여(Participation) 데이터를 조회하고, 이를 여러 엔티티를 조인(join)하여 그룹화(groupBy) 및 프로젝션(projection)을 통해 원하는 형태의 DTO로 변환합니다.
{: .prompt-info}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>
```java
@Override
public List<ParticipationResponse> findParticipationListByCompetitionId(Integer competitionId) {

  return queryFactory.select(QDivision.division.divisionId,
      QDivision.division.divisionName,
      QDivision.division.participationCompetitions,
      QPARTICIPATIONCOMPETITION.user,
      QParticipationCompetitionFile.participationCompetitionFile

    )
    .from(QDivision.division)
    .join(QDivision.division.participationCompetitions, QPARTICIPATIONCOMPETITION)
    .leftJoin(QPARTICIPATIONCOMPETITION.participationCompetitionFiles, QParticipationCompetitionFile.participationCompetitionFile)
    .join(QPARTICIPATIONCOMPETITION.user, QUser.user)
    .where(QDivision.division.competition.competitionId.eq(competitionId))
    .orderBy(QPARTICIPATIONCOMPETITION.createdAt.desc())
    .transform(
      groupBy(QDivision.division.divisionId)
        .list(Projections.fields(ParticipationResponse.class,
          QDivision.division.divisionId,
          QDivision.division.divisionName,

          GroupBy.list(Projections.fields(ParticipationResponse.ParticipationDto.class,

            QPARTICIPATIONCOMPETITION.participationCompetitionId.as("participationId"),
            QPARTICIPATIONCOMPETITION.name,
            QPARTICIPATIONCOMPETITION.phoneNum,
            QPARTICIPATIONCOMPETITION.email,
            QPARTICIPATIONCOMPETITION.createdAt,
            QPARTICIPATIONCOMPETITION.updatedAt,
            Projections.fields(ParticipationResponse.ParticipationDto.ApplicantInfo.class,
              QPARTICIPATIONCOMPETITION.user.userId,
              QPARTICIPATIONCOMPETITION.user.name
            ).as("applicantInfo"),
            Projections.fields(ParticipationResponse.ParticipationDto.File.class,
              QParticipationCompetitionFile.participationCompetitionFile.fileName,
              QParticipationCompetitionFile.participationCompetitionFile.filePath
            ).as("file")
          )).as("participationList")
        )));
}
```
<br>

---

### 주요 구성 요소

- **QDivision.division**
  - 주된 엔티티로, 대회(Competition)와 관련된 구분(Division) 정보를 담당합니다.

- **QPARTICIPATIONCOMPETITION**
  - Division과 연관된 참여(Participation) 정보를 조회하기 위한 엔티티입니다.

- **QParticipationCompetitionFile**
  - 참여 관련 파일 정보를 조회하기 위한 엔티티로, 참여와 `left join`을 사용하여 파일 데이터가 없는 경우에도 결과에 포함시킵니다.

- **QUser.user**
  - 참여 정보를 등록한 사용자(User)의 정보를 조회하기 위해 사용합니다.

---

### 쿼리 단계별 설명

1. **Select 절**
  - `queryFactory.select(...)`
  - `Division`의 `divisionId`, `divisionName`, 그리고 연관된 `participationCompetitions`, 참여한 사용자의 정보, 참여 파일 정보를 선택합니다.

2. **From 및 Join**
  - `from(QDivision.division)`
    - 기본 엔티티로 Division을 선택합니다.
  - `join(QDivision.division.participationCompetitions, QPARTICIPATIONCOMPETITION)`
    - Division과 연결된 Participation 엔티티를 내부 조인합니다.
  - `leftJoin(QPARTICIPATIONCOMPETITION.participationCompetitionFiles, QParticipationCompetitionFile.participationCompetitionFile)`
    - 참여 엔티티와 관련된 파일 정보를 외부 조인(Left Join)하여 파일이 없는 경우에도 데이터를 유지합니다.
  - `join(QPARTICIPATIONCOMPETITION.user, QUser.user)`
    - 참여 정보를 등록한 사용자 정보를 가져옵니다.

3. **Where 절**
  - `.where(QDivision.division.competition.competitionId.eq(competitionId))`
  - 전달받은 `competitionId`와 일치하는 Division만 필터링합니다.

4. **정렬 (Order By)**
  - `.orderBy(QPARTICIPATIONCOMPETITION.createdAt.desc())`
  - 참여 생성일자를 기준으로 내림차순 정렬합니다.

5. **그룹화 및 변환 (Transform)**
  - `.transform(groupBy(QDivision.division.divisionId).list(...))`
  - Division의 `divisionId`를 기준으로 그룹화합니다.
  - 각 그룹별로 `ParticipationResponse` DTO를 생성하며,
    - **Division 정보**: `divisionId`, `divisionName`
    - **참여 목록**:
      - `GroupBy.list`를 사용하여 각 참여에 대해 `ParticipationDto` DTO를 생성
        - 참여의 기본 정보 (참여 ID, 이름, 연락처, 이메일, 생성 및 수정일자)
        - **중첩 DTO**:
          - `ApplicantInfo`: 참여한 사용자 정보 (`userId`, `name`)
          - `File`: 참여 파일 정보 (`fileName`, `filePath`)

---

### 요약

- **조인**: 여러 엔티티 간의 관계를 조인하여 필요한 데이터를 모두 가져옵니다.
- **필터링**: Competition ID를 기준으로 원하는 Division을 선택합니다.
- **정렬**: 참여 데이터는 최신 순으로 정렬되어 있습니다.
- **그룹화 및 프로젝션**: QueryDSL의 강력한 그룹화 기능을 사용해 Division별로 참여 데이터를 DTO에 맞게 변환합니다.

이와 같이 복잡한 쿼리를 단일 메서드로 작성함으로써, 클라이언트에 필요한 데이터 구조(계층형 DTO)를 효율적으로 반환할 수 있습니다.


---

### 고민
> 여기서 리스트안에 또 1대다 매핑으로 그룹화가 필요하다.
{: .prompt-warning}

<br>

---


# 해결 방식
> 우선 중복값이 생기더라도 값을 가져온 후 애플리케이션 레벨에서 제거하며 컬렉션으로 만들어 주기로 하였다.
{: .prompt-tip}

## for문을 통한 1대다 첨부파일 그룹화 방식
> 이 메서드는 쿼리 결과로 받은 `ParticipationResponse` 객체 내의 참여 요청 리스트에서, 하나의 참여 항목에 여러 첨부파일이 매핑되어 있는 경우를 그룹화하기 위한 애플리케이션 레벨의 처리 방식입니다.
{: .prompt-info}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div> 

```java
 public List<ParticipationResponse> getParticipateListByCompetitionId(Integer competitionId) {
  List<ParticipationResponse> results = participationCompetitionRepository.findParticipationListByCompetitionId(competitionId);
  return  groupFilesByParticipationId(results);
}

private List<ParticipationResponse> groupFilesByParticipationId(List<ParticipationResponse> results){
        
  for(ParticipationResponse result:results){// 리스트 분해
    List<ParticipationResponse.ParticipationDto> participationList = result.getParticipationList();//for 문 안 현재 대회의 리스트
    Map<Long, Integer> mainIdsAndIndices  = new HashMap<>();//메인이될 아이디와 그 객체의 인덱스번호

    for(int i=0; i<participationList.size(); i++){//현재 대회의 요청 리스트를 돔 i는 index 번호
      ParticipationResponse.ParticipationDto participation = participationList.get(i);
      Long participationId = participation.getParticipationId();//for 문 안 현재 요청의 아이디
      if (participation.getFile().getFilePath()==null) {// 파일주소가 null 이라면 파일이 없는 요청이므로 다음 요청으로 넘어감
        participationList.get(i).setFiles(null);
        continue;// 파일이 없으므로 중복값도 없으므로 그냥 넘어감
      } else if (mainIdsAndIndices.containsKey(participationId)) {// 이미 중복된 값이 있다면
        Integer mainIndex = mainIdsAndIndices.get(participationId);//메인이될 객체의 index 넘버
        participationList.get(mainIndex).getFiles().add(participation.getFile());//메인객체에 파일을 추가
        participationList.remove(i);//현재 객체 제거
        i--;//한개가 제거되었으므로 인덱스 넘버 보정
        continue;
      }
      //파일은 있는데 첫번째로 나온 요청 id 라면 
      participation.getFiles().add(participationList.get(i).getFile());//new Array List 필요없음 transform 할때 생성되었음
      mainIdsAndIndices.put(participationId, i);//추후 반복문에서 확인을위해 메인의 id와 index 번호 저장
    }
  }
  return results;
}

```

<br>

---

### 동작 원리

1. **리스트 분해**
  - 외부 리스트 `results`를 순회하며, 각 대회별 참여 정보를 담은 `ParticipationResponse` 객체를 가져옵니다.
  - 각 객체 내부의 `participationList`에는 참여 요청들이 포함되어 있습니다.

2. **메인 객체 관리**
  - 중복된 참여 요청이 있을 경우, 하나의 메인 객체에 첨부파일들을 합쳐야 합니다.
  - 이를 위해 `mainIdsAndIndices` 맵을 사용하여, 이미 처리한 참여 항목의 ID와 해당 객체의 인덱스를 저장합니다.

3. **첨부파일 그룹화 로직**
  - **파일이 없는 경우**:
    - 참여 요청 객체의 파일 경로가 `null`이면, 해당 요청에 파일이 없으므로 파일 정보를 `null`로 설정하고 다음 요청으로 넘어갑니다.
  - **중복된 참여 항목 처리**:
    - 이미 `mainIdsAndIndices`에 존재하는 참여 ID인 경우, 기존(메인) 객체의 파일 목록에 현재 객체의 파일 정보를 추가합니다.
    - 이후, 현재 객체는 리스트에서 제거하고 인덱스 보정을 위해 `i`를 감소시킵니다.
  - **첫 등장하는 참여 항목**:
    - 아직 그룹화되지 않은 참여 ID라면, 자신의 파일 정보를 추가한 후, `mainIdsAndIndices`에 해당 참여 ID와 인덱스를 등록합니다.

4. **최종 반환**
  - 모든 대회별 `ParticipationResponse` 객체에 대해 그룹화 처리를 완료한 후, 결과 리스트를 반환합니다.

<br>

---

## 기타 - `Projections`과 `transform` 을 활용한 로직 들 (ex..

```java
.transform(GroupBy.groupBy(qCompetition.competitionId)
                .list(
                        Projections.fields(GetCompetitionAdminListResponse.class,
                                qCompetition.competitionId,
                                qCompetition.user.email.as("userEmail"),
                                qCompetition.phase,
                                qCompetition.competitionName,
                                qCompetition.startDate,
                                qCompetition.endDate,
                                qCompetition.content,
                                qCompetition.relatedUrl.as("link"),
                                qCompetition.competitionStatus.as("status"),
                                qCompetition.createAt,
                                qCompetition.updateAt,
                                qCompetition.deleteAt,
                                GroupBy.set(QDivision.division.divisionName).as("divisions"),
                                GroupBy.set(Projections.fields(CompetitionDetailAttachedFile.class,
                                        QCompetitionAttachedFile.competitionAttachedFile.competitionAttachedFileId,
                                        QCompetitionAttachedFile.competitionAttachedFile.filePath,
                                        QCompetitionAttachedFile.competitionAttachedFile.fileName).skipNulls()).as("files")
                        )));
```
```java
return queryFactory.select(qCompetition.competitionId,
                qCompetition.competitionName,
                qCompetition.divisions,
                qCompetition.competitionAttachedFiles)
                .from(qCompetition)
                .leftJoin(qCompetition.divisions, QDivision.division)
                .leftJoin(qCompetition.competitionAttachedFiles, QCompetitionAttachedFile.competitionAttachedFile)
                .transform(GroupBy.groupBy(qCompetition.competitionId)
                        .list(
                                Projections.fields(GetCompetitionAdminListResponse.class,
                                        qCompetition.competitionId,
                                        qCompetition.competitionName,
                                        GroupBy.set(QDivision.division.divisionName).as("divisions"),
                                        GroupBy.set(Projections.fields(CompetitionDetailAttachedFile.class,
                                                QCompetitionAttachedFile.competitionAttachedFile.competitionAttachedFileId,
                                                QCompetitionAttachedFile.competitionAttachedFile.filePath,
                                                QCompetitionAttachedFile.competitionAttachedFile.fileName).skipNulls()).as("files")

                                )));
```
```java
 queryFactory
  .select(Projections.fields(GetCompetitionAdminListResponse.class,
                       qCompetition.competitionId,
                       qCompetition.user.email.as("userEmail"),
                       qCompetition.phase,
                       qCompetition.competitionName,
                       qCompetition.startDate,
                       qCompetition.endDate,
                       qCompetition.content,
                       qCompetition.relatedUrl.as("link"),
                       qCompetition.competitionStatus.as("status"),
                       qCompetition.createAt,
                       qCompetition.updateAt,
                       qCompetition.deleteAt
               ))
               .from(qCompetition);
```

# Campus Task Planner 요구사항 분석서

문서번호 : SE-2022128023-260507-hw4-001  
소 속 : 한국항공대학교 소프트웨어학과  
작 성 자 : 2022128023 유지윤  

---

## 제/개정 이력

| 버전 | 날짜 | 작성자 | 제/개정사항 | 비고 |
|---|---|---|---|---|
| 1.0 | 2026.05.07 | 유지윤 | 요구사항 분석서 초안 작성 | 최초 작성 |

---

## 목차

1. 서론  
1.1 문서의 목적 및 범위  
1.2 용어 정의  
1.3 참조 문서  

2. 시스템 개요  
2.1 소프트웨어 문맥도  
2.2 기능 분류 및 설명  

3. 요구사항 분석 및 명세  
3.1 정적 분석  
3.2 Use Case Description  
3.3 CRC 카드  
3.4 동적 분석  

5. 인터페이스 분석
4.1 사용자 인터페이스
4.2 시스템 간 연계 인터페이스
4.3 입력 / 출력 인터페이스


6. 제약사항 및 요구사항 추적  
5.1 제약사항  
5.2 요구사항 추적표  

7. 참고문헌 및 부록  

---

## 1. 서론

### 1.1 문서의 목적 및 범위

본 문서는 Campus Task Planner 시스템의 요구사항을 분석하고 명세하는 것을 목적으로 한다.

Campus Task Planner는 대학생을 위한 학업 중심 일정 관리 시스템으로, 과제, 시험 일정, 개인 일정 등을 통합적으로 관리할 수 있도록 지원한다.

본 문서는 기능적 요구사항, 인터페이스 요구사항, 객체 분석, 동적 분석 및 제약사항 등을 정의하며 이후 설계 및 구현 단계의 기준 문서로 활용한다.

---

### 1.2 용어 정의

본 문서의 이해를 돋기 위해 사용된 모든 용어 및 약어를 설명하고 정의합니다.

| 용어 | 설명 |
|---|---|
| 일정 | 과제, 시험, 미팅, 개인 약속 등 관리 대상 |
| 과목 | 대학 수업 단위 |
| 사용자 | 시스템을 사용하는 대학생 |
| API | 시스템 간 데이터 통신 인터페이스 |
| 캘린더 | 날짜 기반 일정 조회 기능 |

---

### 1.3 참조 문서

- hw1_2022128023_유지윤.pdf
- hw2_2022128023_유지윤.pdf
- hw3_2022128023_유지윤.pdf
- 프로젝트 문서양식.docx
- Sample-과제4.요구사항분석서.hwp

---

## 2. 시스템 개요

### 2.1 소프트웨어 문맥도

#### Actor Table

| Actor | Role |
|---|---|
| 사용자 | 시스템 기능을 사용하는 대학생 |
| 시스템 | 일정 등록 및 조회 기능 제공 |
| 데이터베이스 | 일정 데이터 저장 및 관리 |

---

### 2.2 기능 분류 및 설명

| 기능 ID | 기능명 | 설명 |
|---|---|---|
| FR-01 | 회원가입 및 로그인 | 사용자 인증 기능 제공 |
| FR-02 | 일정 등록 | 과제 및 개인 일정 등록 |
| FR-03 | 일정 수정 및 삭제 | 등록된 일정 관리 |
| FR-04 | 진행 상태 관리 | 일정 진행 상태 설정 |
| FR-05 | 캘린더 조회 | 날짜별 일정 조회 |
| FR-06 | 일정 저장 | 데이터 저장 및 불러오기 |
| FR-07 | 친구 관리 | 친구 추가 및 목록 관리 |
| FR-08 | 일정 공유 | 친구 및 팀원과 일정 공유 |
| FR-09 | 일정 알림 | 일정 시작 전 알림 제공 |

---

## 3. 요구사항 분석 및 명세

### 3.1 정적 분석

#### 주요 클래스

| 클래스명 | 설명 |
|---|---|
| User | 사용자 정보 관리 |
| Subject | 과목 정보 관리 |
| Schedule | 일정 정보 관리 |
| Calendar | 캘린더 조회 기능 |
| ScheduleManager | 일정 등록, 수정, 삭제 및 상태 변경을 처리한다. |
| Database | 데이터 저장 및 조회 |
| FriendManager | 친구 추가 및 친구 목록 관리 |
| NotificationManager | 일정 알림 기능 처리 |
| TeamSchedule | 팀 일정 관리 |

---

#### 클래스 관계

- User는 여러 개의 Schedule을 생성할 수 있다.
- Schedule은 여러 개의 Schedule과 연결될 수 있다.
- Calendar는 저장된 Schedule 데이터를 조회한다.
- ScheduleManager는 User의 요청을 처리하고 Database와 연동한다.
- Database는 사용자 및 일정 데이터를 저장한다.
- User는 여러 명의 친구와 연결될 수 있다.
- TeamSchedule은 여러 User와 공유될 수 있다.
- NotificationManager는 Schedule 데이터를 기반으로 알림을 전송한다.

---

### 3.2 Use Case Description

#### Use Case Name : 회원가입 및 로그인을 한다.

| 항목 | 내용 |
|---|---|
| ID | U_01 |
| Importance Level | High |
| Primary Actor | 사용자 |
| Use Case Type | Detail, Essential |
| Brief Description | 사용자가 회원가입 및 로그인 기능을 수행한다. |

#### Stakeholders and Interests

사용자: 자신의 일정을 안전하게 관리하기 위해 로그인 기능을 원한다.

#### Trigger

사용자가 로그인 버튼을 누른다.

#### Relationships

Association : 사용자

#### Normal Flow of Events

1. 사용자는 아이디와 비밀번호를 입력한다.
2. 사용자는 로그인 버튼을 누른다.
3. 시스템은 사용자 정보를 확인한다.
4. 로그인 성공 시 메인 화면으로 이동한다.

#### Alternate / Exceptional Flows

- 입력값이 비어 있는 경우 오류 메시지를 출력한다.
- 로그인 정보가 올바르지 않은 경우 로그인에 실패한다.

---

#### Use Case Name : 과목별 일정을 등록한다.

| 항목 | 내용 |
|---|---|
| ID | U_02 |
| Importance Level | High |
| Primary Actor | 사용자 |
| Use Case Type | Detail, Essential |
| Brief Description | 사용자가 새로운 일정을 등록한다. |

#### Stakeholders and Interests 

사용자: 학업 일정을 체계적으로 관리하기를 원한다.

#### Trigger

사용자가 일정 등록 버튼을 누른다.

#### Relationships

Association : 사용자

#### Normal Flow of Events

1. 사용자는 일정 등록 화면에 접근한다.
2. 사용자는 일정 제목 및 날짜를 입력한다.
3. 사용자는 저장 버튼을 누른다.
4. 시스템은 일정을 저장한다.

#### Alternate / Exceptional Flows

- 필수 입력값이 비어 있는 경우 저장에 실패한다.
- 날짜 형식이 올바르지 않은 경우 오류 메시지를 출력한다.

---

#### Use Case Name : 개인 일정을 등록한다.

| 항목 | 내용 |
|---|---|
| ID | U_03 |
| Importance Level | Medium |
| Primary Actor | 사용자 |
| Use Case Type | Detail, Essential |
| Brief Description | 사용자가 등록된 일정을 조회한다. |

#### Stakeholders and Interests

사용자: 학업 외 개인 일정을 함께 관리하기를 원한다.

#### Trigger

사용자가 개인 일정 등록 버튼을 누른다.

#### Relationships

Association : 사용자

#### Normal Flow of Events

1. 사용자는 캘린더 화면에 접근한다.
2. 시스템은 저장된 일정 데이터를 조회한다.
3. 시스템은 날짜별 일정을 출력한다.

#### Alternate / Exceptional Flows

- 입력값이 누락된 경우 저장이 실패한다.

---

#### Use Case Name : 일정을 수정 및 삭제한다.

| 항목 | 내용 |
|---|---|
| ID | U_04 |
| Importance Level | High |
| Primary Actor | 사용자 |
| Use Case Type | Detail, Essential |
| Brief Description | 사용자가 등록된 일정을 수정하거나 삭제한다. |

#### Stakeholders and Interests

사용자: 등록된 일정을 자유롭게 수정 및 삭제하기를 원한다.

#### Trigger

사용자가 일정 관리 화면에 접근한다.

#### Relationships

Association : 사용자

#### Normal Flow of Events

1. 사용자는 수정 또는 삭제할 일정을 선택한다.
2. 가용자는 수정 또는 삭제 기능을 선택한다.
3. 수정 시 새로운 내용을 입력한다.
4. 시스템은 변경사항을 저장한다.

#### Alternate / Exceptional Flows

- 존재하지 않는 일정 선택 시 오류 메시지를 출력한다.

---

#### Use Case Name : 진행 상태를 관리한다.

| 항목 | 내용 |
|---|---|
| ID | U_05 |
| Importance Level | Medium |
| Primary Actor | 사용자 |
| Use Case Type | Detail, Essential |
| Brief Description | 사용자가 일정의 진행 상태를 설정한다. |

#### Stakeholders and Interests

사용자: 일정 진행 상황을 한눈에 확인하기를 원한다.

#### Trigger

사용자가 상태 변경 버튼을 누른다.

#### Relationships

Association : 사용자

#### Normal Flow of Events

1. 사용자는 일정을 선택한다.
2. 사용자는 예정 / 진행 중 / 완료 상태 중 하나를 선택한다.
3. 시스템은 상태 정보를 저장한다.

#### Alternate / Exceptional Flows

- 저장 중 오류가 발생하면 상태 변경에 실패한다.

---

#### Use Case Name : 캘린더 기반으로 일정을 조회한다.

| 항목 | 내용 |
|---|---|
| ID | U_06 |
| Importance Level | High |
| Primary Actor | 사용자 |
| Use Case Type | Detail, Essential |
| Brief Description | 사용자가 캘린더 형태로 일정을 조회한다. |

#### Stakeholders and Interests

사용자: 날짜별 일정을 직관적으로 확인하기를 원한다.

#### Trigger

사용자가 캘린더 화면에 접근한다.

#### Relationships

Association : 사용자

#### Normal Flow of Events

1. 사용자는 캘린더 화면에 접근한다.
2. 시스템은 저장된 일정 데이터를 조회한다.
3. 시스템은 날짜별 일정 정보를 출력한다. 

#### Alternate / Exceptional Flows

- 저장된 일정이 없는 경우 빈 캘린더를 출력한다. 

---

#### Use Case Name : 일정 데이터를 저장하고 불러온다.

| 항목 | 내용 |
|---|---|
| ID | U_07 |
| Importance Level | High |
| Primary Actor | 시스템 |
| Use Case Type | Detail, Essential |
| Brief Description | 시스템이 일정 데이터를 저장 및 불러온다. |

#### Stakeholders and Interests

사용자: 등록된 일정 데이터가 안전하게 유지되기를 원한다.

#### Trigger

사용자가 일정 등록 또는 조회 기능을 수행한다.

#### Relationships

Association : 시스템

#### Normal Flow of Events

1. 시스템은 입력된 일정 데이터를 저장한다.
2. 사용자가 조회 요청 시 데이터를 불러온다.
3. 시스템은 저장된 데이터를 출력한다.

#### Alternate / Exceptional Flows

- 데이터 저장 실패 시 오류 메시지를 출력한다.
- 데이터베이스 연결 실패 시 조회가 불가능하다.

---

### 3.3 CRC 카드

---

#### Class Name : User

| 항목 | 내용 |
|---|---|
| ID | C_01 |
| Type | Concrete, Domain |
| Description | 시스템 사용자 정보를 관리한다. |
| Associated Use Case | U_01, U_02, U_03, U_04, U_05, U_06 |

#### Responsibilities
- 로그인 요청
- 일정 등록 요청
- 일정 조회 요청
- 진행 상태 변경 요청

#### Collaborators
- Schedule
- Calendar
- ScheduleManager

#### Attributes

| 속성명 | 타입 |
|---|---|
| user_id | String |
| password | String |
| name | String |

---

#### Class Name : Subject

| 항목 | 내용 |
|---|---|
| ID | C_02 |
| Type | Concrete, Domain |
| Description | 과목 정보를 관리한다. |
| Associated Use Case | U_02 |

#### Responsibilities
- 과목 정보 저장
- 과목 정보 조회

#### Collaborators
- Schedule

#### Attributes

| 속성명 | 타입 |
|---|---|
| subject_name | String |
| professor_name | String |

---

#### Class Name : Schedule

| 항목 | 내용 |
|---|---|
| ID | C_03 |
| Type | Concrete, Domain |
| Description | 일정 정보를 저장 및 관리한다. |
| Associated Use Case | U_02, U_03, U_04, U_05 |

#### Responsibilities
- 일정 저장
- 일정 수정
- 일정 삭제
- 일정 상태 변경

#### Collaborators
- User
- Database

#### Attributes

| 속성명 | 타입 |
|---|---|
| schedule_id | Integer |
| title | String |
| date | Date |
| priority | Integer |
| status | String |
| description | String |

---

#### Class Name : Calendar

| 항목 | 내용 |
|---|---|
| ID | C_04 |
| Type | Concrete, Domain |
| Description | 캘린더 기반 일정 조회 기능을 제공한다. |
| Associated Use Case | U_06 |

#### Responsibilities
- 날짜별 일정 조회
- 일정 목록 출력

#### Collaborators
- Schedule

#### Attributes

| 속성명 | 타입 |
|---|---|
| current_month | Integer |
| schedule_list | List |

---

#### Class Name : ScheduleManager

| 항목 | 내용 |
|---|---|
| ID | C_05 |
| Type | Control |
| Description | 일정 관련 기능을 처리한다. |
| Associated Use Case | U_02, U_04, U_05 |

#### Responsibilities
- 일정 등록 처리
- 일정 수정 처리
- 일정 삭제 처리
- 진행 상태 변경 처리

#### Collaborators
- User
- Schedule
- Database

#### Attributes

| 속성명 | 타입 |
|---|---|
| request_data | Object |

---

#### Class Name : Database

| 항목 | 내용 |
|---|---|
| ID | C_06 |
| Type | Entity |
| Description | 사용자 및 일정 데이터를 저장한다. |
| Associated Use Case | U_07 |

#### Responsibilities
- 데이터 저장
- 데이터 조회
- 데이터 수정
- 데이터 삭제

#### Collaborators
- User
- Schedule

#### Attributes

| 속성명 | 타입 |
|---|---|
| connection_info | String |
| stored_data | Object |

---

#### Class Name : FriendManager

| 항목 | 내용 |
|---|---|
| ID | C_07 |
| Type | Control |
| Description | 친구 추가 및 관리 기능을 처리한다. |
| Associated Use Case | U_07 |

#### Responsibilities
- 친구 추가 처리
- 친구 목록 조회
- 친구 삭제 처리

#### Collaborators
- User

#### Attributes

| 속성명 | 타입 |
|---|---|
| friend_list | List |

---

#### Class Name : NotificationManager

| 항목 | 내용 |
|---|---|
| ID | C_08 |
| Type | Control |
| Description | 일정 알림 기능을 처리한다. |
| Associated Use Case | U_08 |

#### Responsibilities
- 일정 알림 전송
- 알림 시간 관리

#### Collaborators
- Schedule
- User

#### Attributes

| 속성명 | 타입 |
|---|---|
| notification_time | DateTime |

---

### 3.4 동적 분석

#### 3.4.1 회원가입 및 로그인 과정
1. 사용자가 로그인 화면에 접근한다.
2. 사요자가 아이디와 비밀번호를 입력한다.
3. 시스템은 입력 정보를 검증한다.
4. 로그인 성공 시 메인 화면으로 이동한다.
5. 로그인 실패 시 오류 메시지를 출력한다.

---

#### 3.4.2 일정 등록 과정
1. 사용자가 일정 등록 화면에 접근한다.
2. 사용자가 일정 정보를 입력한다.
3. 시스템은 입력값을 검증한다.
4. 시스템은 일정 데이터를 저장한다.
5. 저장 완료 후 캘린더에 반영한다.

---


#### 3.4.3 일정 수정 및 삭제 과정
1. 사용자가 수정 또는 삭제할 일정을 선택한다.
2. 사용자가 수정 똔느 삭제 기능을 선택한다.
3. 시스템은 선택된 일정 정보를 처리한다.
4. 수정 또는 삭제 결과를 저장한다.

---


#### 3.4.4 일정 조회 과정
1. 사용자가 캘린더 화면에 접근한다.
2. 시스템은 저장된 일정 데이터를 조회한다.
3. 시스템은 날짜별 일정을 출력한다.

---

#### 3.4.5 일정 공유 과정
1. 사용자가 공유할 일정을 선택한다.
2. 사용자가 친구 또는 팀원을 선택한다.
3. 시스템은 공유 요청을 처리한다.
4. 공유된 일정이 상대방 캘린더에 반영된다.

---

#### 3.4.6 일정 알림 과정
1. 사용자가 알림 시간을 설정한다.
2. 시스템은 설정된 시간을 저장한다.
3. 일정 시작 전에 사용자에게 알림을 전송한다.

---

## 4. 인터페이스 분석

### 4.1 사용자 인터페이스

| 화면 | 설명 |
|---|---|
| 로그인 화면 | 사용자 인증 수행 |
| 회원가입 화면 | 사용자 계정 생성 기능 제공 |
| 일정 등록 화면 | 일정 입력 기능 제공 |
| 캘린더 화면 | 일정 조회 기능 제공 |
| 일정 상세 화면 | 일정 상세 정보 출력 |
| 친구 관리 화면 | 친구 추가 및 목록 조회 |
| 팀 일정 화면 | 공유 일정 관리 |
| 알림 설정 화면 | 일정 알림 설정 |

---

### 4.2 시스템 간 연계 인터페이스

| 인터페이스 | 설명 |
|---|---|
| REST API | 클라이언트와 서버 간 데이터 통신 |
| Database 연동 | 일정 데이터 저장 및 조회 |
| 인증 시스템 | 사용자 로그인 인증 처리 |

---

### 4.3 입력 / 출력 인터페이스

#### 입력 인터페이스

| 입력 항목 | 설명 |
|---|---|
| 일정 제목 | 일정 이름 |
| 날짜 | 일정 날짜 |
| 중요도 | 일정 우선순위 |
| 상세 내용 | 일정 설명 |
| 상태 | 예정 / 진행 중 / 완료 |

#### 출력 인터페이스

| 출력 항목 | 설명 |
|---|---|
| 일정 목록 | 저장된 일정 출력 |
| 캘린더 조회 | 날짜별 일정 조회 |
| 진행 상태 | 일정 상태 출력 |
| 오류 메시지 | 입력 오류 및 저장 실패 안내 |

---

## 5. 제약사항 및 요구사항 추적

### 5.1 제약사항

#### 기술적 제약사항
- macOS 환경 기반 개발
- JavaScript / Python 기반 개발
- MySQL 데이터베이스 사용
- GitHub 기반 형상 관리 수행

#### 운영적 제약사항
- 학기 내 프로젝트 완료 필요
- 사용자 데이터 보호 필요
- 안정적인 일정 저장 기능 필요

---

### 5.2 요구사항 추적표

| 요구사항 ID | 설명 | 관련 Use Case |
|---|---|---|
| FR-01 | 회원가입 및 로그인 | U_01 |
| FR-02 | 일정 등록 | U_02 |
| FR-03 | 일정 조회 | U_03 |
| FR-04 | 진행 상태 관리 | U_02 |
| FR-05 | 캘린더 조회 | U_03 |
| FR-06 | 일정 데이터 저장 | U_02 |
| FR-07 | 친구 관리 | U_07 |
| FR-08 | 일정 공유 | U_08 |
| FR-09 | 일정 알림 | U_09 |

---

## 6. 참고문헌 및 부록

- hw1_2022128023_유지윤.pdf
- hw2_2022128023_유지윤.pdf
- hw3_2022128023_유지윤.pdf
- Sample-과제4.요구사항분석서.hwp
- GitHub Repository

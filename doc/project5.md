# 요구사항 분석서

# Mini Drive System

문서번호 : 요구사항분석서_260514_Doc001  

소 속 :  
팀 명 :  
팀 원 :  
교 수 :  

---

# 제/개정 이력

| 버전 | 날짜 | 작성자 성명 | 제/개정사항 | 비고 |
|:--|:--|:--|:--|:--|
| 1.0 | 2026-05-14 |  | 요구사항 분석서 | 최초 작성 |

---

# 목 차

1. 서론  
1.1 목적 및 범위  
1.2 용어 정의  
1.3 참조 문서  

2. 시스템 개요  
2.1 소프트웨어 문맥도
2.2 기능 분류 및 설명

3. 요구사항 명세  
3.1 정적 분석  
3.2 CRC 카드  
3.3 동적 분석  

5. 인터페이스 분석  

6. 제약사항  

7. 요구사항 추적표  

8. 참고문헌 및 부록  

---

# 1. 서론

## 1.1 목적 및 범위

이 문서는 조직 내 파일을 중앙에서 관리하고 사용자 간 파일 공유를 지원하는 Mini Drive System 프로젝트의 요구사항을 분석하고 정의하기 위한 문서이다.  

본 문서는 객체지향 분석 기법과 UML 기반 모델링을 이용하여 시스템의 기능적 요구사항을 분석하며, 기능 모델링, 구조 모델링, 행위 모델링을 수행한다.

---

## 1.2 용어 정의

| 용어 | 설명 |
|:--|:--|
| 클라우드 파일 시스템 | 네트워크 기반 파일 저장 및 공유 시스템 |
| API | 응용 프로그램 기능을 제어하기 위한 인터페이스 |
| 버전 관리 | 파일 변경 이력을 저장하고 관리하는 기능 |
| UML | 객체지향 모델링을 위한 표준 모델링 언어 |
| Use Case | 시스템이 제공하는 사용자 중심 기능 |

---

## 1.3 참조 문서

- 프로젝트 정의서  
- 프로젝트 관리 계획서  
- 요구사항 정의서  

---

# 2. 시스템 개요

## 2.1 소프트웨어 컨텍스트(Context)

Mini Drive System은 사용자가 웹 환경에서 파일을 업로드, 다운로드 및 공유할 수 있도록 지원하는 클라우드 기반 파일 관리 시스템이다.  

시스템은 사용자 인증 기능과 파일 버전 관리 기능을 제공하며, 사용자 간 협업을 지원한다.

---

## 2.1.1 Actor Table

| Actor | Role |
|:--|:--|
| 사용자 | 파일 업로드, 다운로드, 검색 및 공유 기능을 사용하는 사용자 |
| 관리자 | 사용자 및 파일 권한을 관리하는 사용자 |
| 인증 시스템 | 사용자 로그인 인증을 처리하는 외부 시스템 |

---

## 2.1.2 UseCase Diagram

### 액터와 유스케이스 관계

| 액터 | 유스케이스 |
|:--|:--|
| 사용자 | 회원가입을 한다, 로그인을 한다, 파일을 업로드한다, 파일을 다운로드한다, 파일을 공유한다 |
| 관리자 | 사용자 권한을 관리한다, 파일 권한을 설정한다 |
| 인증 시스템 | 사용자 인증을 수행한다 |

---

## 2.2 기능 분류 및 설명

### 2.2.1 UseCase Description

---

## Use Case Name : 회원가입
ID : U_01  
Importance Level : high

Primary Actor : 사용자  

Use Case Type : Detail, essential

### Brief Description
이 Use-Case는 사용자가 회원가입을 수행하는 기능을 표현한다.

### Stakeholders and Interests
사용자 : 사용자는 시스템을 이용하기 위해 회원가입하기를 원한다.

### Trigger
사용자는 회원가입 버튼을 누른다.

### Relationships

- Association : 사용자  
- Include :  
- Extend :  
- Generalization :  

### Normal Flow of Events

1. 사용자는 아이디, 비밀번호, 이메일 주소를 입력한다.  
2. 사용자는 회원가입 버튼을 누른다.  
3. 시스템은 회원가입 정보를 검증한다.  
4. 시스템은 회원가입 성공 시 로그인 화면으로 이동한다.  

### Subflows

없음

### Alternate / Exceptional Flows

2.a1 : 입력값이 공란인 경우 시스템은 실패 이유를 출력한다.  

2.a2 : 동일한 아이디가 존재하는 경우 시스템은 실패 이유를 출력한다.  

---

## Use Case Name : 로그인
ID : U_02  
Importance Level : high

Primary Actor : 사용자

Use Case Type : Detail, essential

### Brief Description
이 Use-Case는 사용자가 로그인 기능을 수행하는 기능을 표현한다.

### Stakeholders and Interests
사용자 : 사용자는 시스템에 접근하기 위해 로그인하기를 원한다.

### Trigger
사용자는 로그인 버튼을 누른다.

### Relationships

- Association : 사용자  
- Include : 사용자 인증을 수행한다  
- Extend :  
- Generalization :  

### Normal Flow of Events

1. 사용자는 아이디와 비밀번호를 입력한다.  
2. 사용자는 로그인 버튼을 누른다.  
3-1. 로그인에 성공한 경우  
S-1 : 로그인 성공  

3-2. 로그인에 실패한 경우  
S-2 : 로그인 실패  

### Subflows

#### S-1 : 로그인 성공

1. 시스템은 메인 화면으로 이동한다.  

#### S-2 : 로그인 실패

1. 시스템은 로그인 실패 이유를 출력한다.  

### Alternate / Exceptional Flows

2.a1 : 입력값이 공란인 경우 오류 메시지를 출력한다.  

---

## Use Case Name : 파일 업로드  
ID : U_03  
Importance Level : high

Primary Actor : 사용자

Use Case Type : Detail, essential

### Brief Description
이 Use-Case는 사용자가 파일을 업로드하는 기능을 표현한다.

### Stakeholders and Interests
사용자 : 사용자는 자신의 파일을 시스템에 저장하기를 원한다.

### Trigger
사용자는 업로드 버튼을 누른다.

### Relationships

- Association : 사용자  
- Include : 파일 저장을 수행한다  
- Extend :  
- Generalization :  

### Normal Flow of Events

1. 사용자는 업로드 버튼을 누른다.  
2. 사용자는 업로드할 파일을 선택한다.  
3. 시스템은 파일 정보를 검증한다.  
4. 시스템은 파일을 저장한다.  
5. 시스템은 업로드 완료 메시지를 출력한다.  

### Subflows

없음

### Alternate / Exceptional Flows

3.a1 : 파일 크기 제한을 초과한 경우 오류 메시지를 출력한다.  

4.a1 : 저장 공간이 부족한 경우 저장 실패 메시지를 출력한다.  

---

## Use Case Name : 파일 다운로드  
ID : U_04  
Importance Level : high

Primary Actor : 사용자

Use Case Type : Detail, essential

### Brief Description
이 Use-Case는 사용자가 파일을 다운로드하는 기능을 표현한다.

### Stakeholders and Interests
사용자 : 사용자는 원하는 파일을 다운로드하기를 원한다.

### Trigger
사용자는 다운로드 버튼을 누른다.

### Relationships

- Association : 사용자  
- Include : 파일 검색을 수행한다  
- Extend :  
- Generalization :  

### Normal Flow of Events

1. 사용자는 다운로드할 파일을 선택한다.  
2. 사용자는 다운로드 버튼을 누른다.  
3. 시스템은 파일 접근 권한을 확인한다.  
4. 시스템은 파일 다운로드를 수행한다.  

### Subflows

없음

### Alternate / Exceptional Flows

3.a1 : 접근 권한이 없는 경우 다운로드를 제한한다.  

---

## Use Case Name : 파일 공유
ID : U_05  
Importance Level : high

Primary Actor : 사용자

Use Case Type : Detail, essential

### Brief Description
이 Use-Case는 사용자가 파일을 다른 사용자와 공유하는 기능을 표현한다.

### Stakeholders and Interests
사용자 : 사용자는 파일을 다른 사용자와 공유하기를 원한다.

### Trigger
사용자는 공유 버튼을 누른다.

### Relationships

- Association : 사용자  
- Include : 파일 검색을 수행한다  
- Extend :  
- Generalization :  

### Normal Flow of Events

1. 사용자는 공유할 파일을 선택한다.  
2. 사용자는 공유 대상을 입력한다.  
3. 시스템은 사용자 정보를 확인한다.  
4. 시스템은 파일 공유 권한을 설정한다.  
5. 시스템은 공유 완료 메시지를 출력한다.  

### Subflows

없음

### Alternate / Exceptional Flows

2.a1 : 존재하지 않는 사용자일 경우 오류 메시지를 출력한다.  

---

# 3. 요구사항 명세

## 3.1 정적 분석

### 객체 식별

| 객체명 | 설명 |
|:--|:--|
| User | 시스템 사용자 정보 |
| File | 파일 정보 관리 |
| Folder | 폴더 정보 관리 |
| Share | 파일 공유 정보 |
| Version | 파일 버전 정보 |
| AuthManager | 사용자 인증 처리 |

---

## 3.2 CRC 카드

---

### Class Name : User  
ID : 01  
Type : Concrete, Domain

### Description
시스템을 사용하는 사용자 정보를 나타낸다.

### Associated Use Case
U_01, U_02, U_03, U_04, U_05

### Responsibilities

- 회원가입 요청() : void  
- 로그인 요청() : void  
- 파일 업로드 요청() : void  
- 파일 다운로드 요청() : void  
- 파일 공유 요청() : void  

### Collaborators

- File  
- Share  
- AuthManager  

### Attributes

- 아이디 : String  
- 비밀번호 : String  
- 이메일 주소 : String  

### Relationships

- Generalization (a-kind-of):  
- Aggregation (has-parts): File  
- Other Associations: Share  

---

### Class Name : File  
ID : 02  
Type : Concrete, Domain

### Description
사용자의 파일 정보를 나타낸다.

### Associated Use Case
U_03, U_04, U_05

### Responsibilities

- 파일 저장() : void  
- 파일 다운로드() : void  
- 파일 삭제() : void  
- 버전 관리() : void  

### Collaborators

- User  
- Version  
- Folder  

### Attributes

- 파일명 : String  
- 파일크기 : Integer  
- 업로드날짜 : Date  

### Relationships

- Generalization (a-kind-of):  
- Aggregation (has-parts): Version  
- Other Associations: User  

---

## 3.3 동적 분석

### 3.3.1 회원가입을 한다.

| 순서 | 액터의 행위 | 시스템의 응답 |
|:--|:--|:--|
| 1 | 회원가입 버튼을 클릭한다 | 회원가입 화면을 출력한다 |
| 2 | 회원 정보를 입력한다 | 입력 정보를 검증한다 |
| 3 | 회원가입 버튼을 누른다 | 회원가입 성공 여부를 출력한다 |

---

### 3.3.2 로그인을 한다.

| 순서 | 액터의 행위 | 시스템의 응답 |
|:--|:--|:--|
| 1 | 아이디와 비밀번호를 입력한다 | 입력 정보를 확인한다 |
| 2 | 로그인 버튼을 누른다 | 인증 시스템과 로그인 정보를 검증한다 |
| 3 | 로그인 성공 시 메인화면으로 이동한다 | 메인 기능을 활성화한다 |

---

### 3.3.3 파일을 업로드한다.

| 순서 | 액터의 행위 | 시스템의 응답 |
|:--|:--|:--|
| 1 | 업로드 버튼을 누른다 | 파일 선택 창을 출력한다 |
| 2 | 업로드할 파일을 선택한다 | 파일 정보를 검증한다 |
| 3 | 업로드를 요청한다 | 파일 저장을 수행한다 |
| 4 | 업로드 완료를 확인한다 | 완료 메시지를 출력한다 |

---

### 3.3.4 파일을 다운로드한다.

| 순서 | 액터의 행위 | 시스템의 응답 |
|:--|:--|:--|
| 1 | 다운로드할 파일을 선택한다 | 파일 정보를 확인한다 |
| 2 | 다운로드 버튼을 누른다 | 다운로드를 수행한다 |
| 3 | 파일 저장 위치를 선택한다 | 다운로드 완료를 출력한다 |

---

### 3.3.5 파일을 공유한다.

| 순서 | 액터의 행위 | 시스템의 응답 |
|:--|:--|:--|
| 1 | 공유할 파일을 선택한다 | 공유 설정 화면을 출력한다 |
| 2 | 공유 대상을 입력한다 | 사용자 정보를 확인한다 |
| 3 | 공유 버튼을 누른다 | 파일 공유 권한을 설정한다 |
| 4 | 공유 완료를 확인한다 | 완료 메시지를 출력한다 |

---

# 4. 인터페이스 분석

없음

---

# 5. 제약사항

- 웹 브라우저 환경에서 동작해야 한다.  
- 사용자 인증 기능이 반드시 필요하다.  
- 파일 공유 시 접근 권한 제어가 가능해야 한다.  
- Windows 및 Linux 환경을 지원해야 한다.  

---

# 6. 요구사항 추적표

| 요구사항 | U_01 | U_02 | U_03 | U_04 | U_05 |
|:--|:--|:--|:--|:--|:--|
| FR_001 | O |  |  |  |  |
| FR_002 |  | O |  |  |  |
| FR_003 |  | O |  |  |  |
| FR_004 |  |  | O |  |  |
| FR_005 |  |  |  | O |  |
| FR_006 |  |  | O |  |  |
| FR_007 |  |  | O |  |  |
| FR_008 |  |  | O |  |  |
| FR_009 |  |  |  |  | O |
| FR_010 |  |  |  | O | O |
| FR_011 |  |  |  | O | O |
| FR_012 |  |  | O | O | O |

---

# 7. 참고문헌 및 부록

- 프로젝트 정의서  
- 프로젝트 관리 계획서  
- 요구사항 정의서  
- ch08 객체지향 분석 강의자료  

---

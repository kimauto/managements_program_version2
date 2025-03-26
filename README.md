# ![header](https://capsule-render.vercel.app/api?type=venom&color=0:5C258D,100:4389A2&height=300&section=header&text=Management%20Sysetem&fontColor=black&fontSize=50&stroke=5C258D&strokeWidth=1)

</div> 

## 소개
학생과 직원에 대한 정보를 관리하는 통합 관리 시스템입니다. 

- 프로젝트 소개
- 개발 기간
- 주요 기능
- 프로젝트 역할
- 프로젝트 클래스 다이어그램
- 기술 스택
- 기술적 이슈와 해결 과정


<br>

## 프로젝트 소개 

### Version1: Student Management System  ![Version1 프로젝트 링크](https://github.com/kimauto/managements_program)

### Version2: Employee Management System ![Version2 프로젝트 링크](https://github.com/kimauto/managements_program_version2)

학생과 직원에 대한 통합 관리시스템을 구현하기 앞서 학생 관리 시스템을 Version1, 직원 관리 시스템을 Version2로 계획해 구현하고 통합했습니다. 

Employee Management System은 직원 정보의 저장, 읽기, 변경, 삭제 기능을 제공하고 직위에 따른 연봉 인상률을 적용했습니다. 

<br>

## 개발 기간
- V2: 2024.2.18(화) ~ 2024.2.21(금): Employee System 설계 및 팀 깃허브 설정

- V2: 2024.2.24(월) ~ 2024.3.5(수): 기능 구현

- V2: 2024.3.6(목) ~ 2024.3.10(월): 리팩토링

<br>

## 주요 기능

- 직원 정보 입력

- 직원 정보 조회

- 직원 정보 삭제

- 직원 정보 수정

- 직원 급여 인상

<br>

## 프로젝트 클래스 다이어그램
### 1. Employee

![image](https://github.com/user-attachments/assets/9023c2b8-3111-48ce-9828-811e786c085d)

### 2. Controller

![image](https://github.com/user-attachments/assets/ff7c7b74-c13d-4e7f-a9ce-a7e261cfe12c)

### 3. SalaryService

![image](https://github.com/user-attachments/assets/46a4cfc7-ba1c-4e94-9bf7-c075dbccd8a0)

### 4. Repository

![image](https://github.com/user-attachments/assets/7739ee3a-5e3d-4c63-86bb-d041b7214c02)

### 5. DB ERD

![image](https://github.com/user-attachments/assets/b47e9455-b64b-47be-a719-ceacd5953cfb)

<br>


## ⚙ 기술 스택

### Back-end
<div>
<img src="https://github.com/yewon-Noh/readme-template/blob/main/skills/Java.png?raw=true" width="80">
<img src="https://github.com/yewon-Noh/readme-template/blob/main/skills/Mysql.png?raw=true" width="80">

</div>

### Tools
<div>
<img src="https://github.com/yewon-Noh/readme-template/blob/main/skills/Github.png?raw=true" width="80">

<br />


<br>

## 🛠️ 기술적 이슈와 해결 과정

---

### 1. DB 민감 정보 유출 문제

- **문제 발생**
    
    DB 접속을 위한 IP 주소와 DB 비밀번호가 포함된 설정 파일을 `.gitignore`에 등록하지 않은 채 `git push`하여, 민감 정보가 GitHub 레포지토리에 노출되는 문제가 발생
    
- **문제 분석**
    
    이후 `.gitignore`에 해당 파일을 추가했지만, 이미 push된 상태이기 때문에 계속해서 버전 관리 대상이 됨
    
- **해결 방법**
    - GitHub에 업로드된 파일의 **캐시 삭제**
    - 이후 `.gitignore`에 해당 파일 추가
- **결과**
    
    **민감 정보 제거 및 재발 방지 완료**
    
- **결론**
    
    **민감한 정보는 처음부터 반드시 `.gitignore`에 등록하자!**
    

---

### 2. GitHub 충돌 및 협업 방식 개선

- **문제 발생**
    
    Version1에서는 Git과 GitHub를 사용하긴 했지만 **효율적인 협업 방식은 적용하지 못함**
    
- **문제 분석**
    
    PR 및 Merge 과정에서의 충돌 관리가 미흡했고, 작업 분배도 명확하지 않았음
    
- **해결 방법**
    - Version2부터는 팀원 간의 **브랜치 전략 수립** (예: `feature/`, `bugfix/`, `hotfix/`)
    - PR 생성 시 **리뷰 및 승인 절차** 명확화
    - **커밋 컨벤션** 및 **Merge 규칙** 적용
- **결과**
    
    **팀 내 협업 체계가 정립되고, 충돌 발생 시 빠르게 원인 파악 및 해결 가능**
    
- **결론**
    
    **Git은 코드 저장 도구 그 이상, 협업 도구로 적극 활용해야 한다**
    

---

### 3. 예외 처리 계층 분리 미숙

- **문제 발생**
    
    초반에는 예외 처리를 어디서 해야 하는지 명확하지 않아, `Repository`, `Service`, `Controller` 계층 어디에 처리해야 할지 혼란스러움 발생
    
- **문제 분석**
    
    
    | 계층 | 역할 |
    | --- | --- |
    | **Repository** | DB 관련 로직 수행 중 `SQLException` 등의 예외 발생 |
    | **Service** | 비즈니스 로직 수행. 예외는 직접 처리하지 않고 상위 계층으로 전달 |
    | **Controller** | 사용자 요청 응답 처리. 최종적으로 예외를 **로깅 + 에러 메시지 응답** |
- **해결 방법**
    - **Repository**: 발생할 수 있는 DB 예외를 `try-catch`로 감싸고, **커스텀 예외**로 변환 후 던짐
    - **Service**: 예외를 다시 `catch`하지 않고, **Controller로 전달**
    - **Controller**: 최상위 계층에서 예외를 받아 **의미 있는 메시지로 응답 처리**
- **결과**
    
    **각 계층의 역할이 명확해지고, 예외 발생 시 책임 있는 위치에서 처리 가능**
    
- **결론**
    
    **예외 처리는 계층에 따라 책임을 나눠서 처리하는 것이 유지보수성과 안정성을 높인다**

   

<br>









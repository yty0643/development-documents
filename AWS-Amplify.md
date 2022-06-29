# AWS Amplify

모바일 및 웹 개발자가 AWS 기반의 풀 스택 어플리케이션을 빠르게 구성하는 방법을 제공한다.<br/>
서버리스 기술 스택을 빠르게 구축할 수 있는 기능을 제공한다.<br/>
코드 배포, 인증, 분석, 데이터베이스 등 다양한 기능을 쉽게 이용할 수 있는 인터페이스를 제공한다.<br/>
일반적인 비즈니스 로직 뿐만 아니라 분석 또는 상호작용, Machine Learning Prediction 등을 위한 어플이케이션의 구축도 가능하다.<br/>
프레임워크에 대해서는 추가비용이 발생하지 않으며 사용한 AWS 서비스에 대해서만 비용을 지불한다. (호스팅 시 비용 발생)<br/>

---

## AWS Amplify 구성 요소

- CLI
- Client Libs(IOS, Android, JS)
- Amplify Console - CI/CD, Hosting

---

## AWS Amplify 사용 과정

1. 플랫폼 선택
   - Android
   - IOS
   - JS (React, Vue ...)
2. AWS 서비스 구성
   - CLI를 통해 구성
   - console에서 따로따로 작업 후 병합 가능
3. App 에 연결
   - Amplify Lib 연결

---

## AWS Amplify CLI

```bash
# Amplify 환경 초기화
$ amplify init

# Amplify를 통해 Cognito User Pool 연동
$ amplify add auth

# Amplify를 통해 Pinpoint 연동
$ amplify add analytics

# Amplify 기반의 백엔드 API 스택을 구성
$ amplify add api

# 스택을 AWS CloudFormation을 통해 배포
# AWS CloudFormation - 인프라 관리 서비스
$ amplify push
```

```bash
$ amplify init
Name :
environment:
Default editor :
Type of add :
Javascript framework :
Source directory path :
Distribution Directory Path :
Build command :
Start command :
```

---

## Amplify를 이용한 인증 구현

### Amazon Cognito

- 웹 및 모바일 환경에 손쉽게 가입, 인증, 로그인 등 구현
- 완전관리형 사용자 디렉토리 제공
- Amazon, Apple, Facebook, Google 등 소셜 자격증명 연동
- SAML 2.0 기반의 엔터프라이즈 자격 증명 연동
- Amplify를 통해 인증 환경을 쉽게 연동 가능

#### User Pools

- 수 백만의 사용자를 위해 확장되는 완전관리형의 User Directory
- 회원 가입, 로그인, 로그아웃 제공하고 이를 바탕으로 인증 가능
- 사용자 계정에 대한 정책 정의 가능
- Lambda 트리거를 통한 사용자 정의 Workflow 연동이 가능

#### Identity pools

- AWS 리소스 접근을 위한 임시 자격 증명을 제공
- 외부 Identity Provider에 대한 권한을 수임해서 작업 처리
- 비회원에 대한 접근 제어가 가능
- 멀티 디바이스 및 멀티 어카운트에 대해 Identity를 통한 관리가 가능

```bash
# Cognito 프로비저닝, default or custom configuration
$ amplify add auth
```

```javascript
import { Auth } from "aws-amplify";

Auth.signin("username", "userpassword");
Auth.currentAuthenticatedUser();
Auth.signOut();
```

---

## Amplify API (백엔드)

일반적인 환경에서 웹 앱 백엔드 구성 시 고려해야 할 다음과 같은 사항을 서버리스 컨셉에 의해 상당부분 AWS의 도움을 받을 수 있고, 비즈니스 로직에 포커스를 맞춰서 진행할 수 있다.

- ~~장애에 대한 복구~~
- ~~로드 밸런싱~~
- ~~웹 서버 스택~~
- ~~어플리케이션 서버 스택~~
- 비즈니스 로직

### Amplify API 기술 스택

<img width="850" alt="api" src="https://user-images.githubusercontent.com/80657819/176343543-4aeea8f4-9619-440d-a0b1-1fe5925b73bb.png">

### Amplify 를 통한 API 접근 방식

<img width="850" alt="접근방식" src="https://user-images.githubusercontent.com/80657819/176344821-c3d6479a-c372-43b0-a4fc-8b584a62b3cf.PNG">

- REST API
  > HTTP URL을 통해 경로를 나누고 URL에 맞는 리소스를 반환
- GraphQL API
  > 하나의 API 엔드포인트로 클라이언트가 데이터베이스에 직접 접근하여 효율적으로 작업을 처리할 수 있도록 하는 새로운 API 접근 방식 (Facebook)

#### Amplify 기반의 REST API 배포

```bash
$ amplify add api
# chose REST with Express backend
# TODO: Code fucntion (함수 작업)
$ amplify push
# 배포완료
```

스택 구성

- Amazon API Gateway
- AWS Lambda (express)

#### AWS AppSync를 통한 API 연동

- 실시간 데이터 동기화 기능이 제공되는 완전 관리형 GraphQL 서비스
- 단일 엔드포인트로 GraphQL을 통해 데이터에 대한 CRUD가 가능
- AppSync는 API 호출 요청에 따라 자동으로 Scaling
- Cognito User Pool 과 연동되어 인증 받은 권한으로 API 수행이 가능

AppSync를 이용한 GraphQL 이용시 다음과 같은 이점이 있다.

- 관리형 서버리스 GraphQL 서비스
- 데이터 소스에 대한 연결을 제공
- 데이터 동기화, 실시간 데이터 접근 등 API 기능을 제공
- AWS 서비스를 위한 GraphQL 인터페이스를 제공
- IAM, Cognito, OIDC등 보안 Feature를 제공

AppSync는 데이터스토어와 연동이 가능. (DynamoDB)

- 어떤 규모에서도 10ms 미만의 성능을 제공하는 Key-value형태의 DB
- 대규모 처리와 분산 환경에서의 성능 최적화
- 사용한 만큼만 비용청구
- 별도의 관리가 필요없는 서버리스 DB
- AppSync의 데이터소스 형태로 연동이 가능

Amplify DataStore

- 디바이스에 저장되는 오프라인 스토리지를 제공한다.
- 오프라인 스토리지는 온라인 상태로 전환 시 자동으로 동기화 된다.

---

## AWS-Amplify를 통한 Web Hosting

1. Git 저장소를 연결
2. 빌드 세팅을 설정
3. 변경 사항을 앱에 배포

Amplify를 통한 웹 호스팅 장점

- 전세계에서 사용 가능한 웹 호스팅을 제공
- 쉽게 Https 도메인 생성이 가능
- 단순한 CI/CD 파이프라인 구축
- Branch 단위 배포가 가능
- 원자 단위 배포(아토믹 디플로이먼트)
  > 운영중인 서비스의 배포가 즉각 반영이되는 컨셉
- 웹 배포를 암호로 보호 가능

Amplify CI/CD

- Amplify는 Git 기반의 풀 스택 서버리스 앱에 대한 CI/CD를 제공한다.
- 코드 변경을 Amplify를 이용해 단일 Workflow로 무중단 배포

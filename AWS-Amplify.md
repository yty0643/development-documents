# AWS Amplify

모바일 및 웹 개발자가 AWS 기반의 풀 스택 어플리케이션을 빠르게 구성하는 방법을 제공한다.<br/>
서버리스 기술 스택을 빠르게 구축할 수 있는 기능을 제공한다.<br/>
코드 배포, 인증, 분석, 데이터베이스 등 다양한 기능을 쉽게 이용할 수 있는 인터페이스를 제공한다.<br/>
일반적인 비즈니스 로직 뿐만 아니라 분석 또는 상호작용, Machine Learning Prediction 등을 위한 어플이케이션의 구축도 가능하다.<br/>
프레임워크에 대해서는 추가비용이 발생하지 않으며 사용한 AWS 서비스에 대해서만 비용을 지불한다. (호스팅 시 비용 발생)<br/>

## AWS Amplify 구성 요소

- CLI
- Client Libs(IOS, Android, JS)
- Amplify Console - CI/CD, Hosting

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

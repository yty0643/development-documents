# AWS

AWS란 아마존닷컴에서 개발한 클라우드 컴퓨팅 플랫폼이다.

AWS는 네트워킹을 기반으로 가상 컴퓨터, 스토리지, 네트워크 인프라 등 다양한 서비스를 제공하고 있다.

비즈니스와 개발자가 웹 서비스를 사용하여 확장 가능하고 정교한 애플리케이션 구축을 도와준다.

소규모 법인 및 개인을 포함한 다양한 사용자들이 사용허고 있으며, 클라우드 컴퓨팅의 장점을 이용하기 위해 거대 기업에서도 활용하고 있다.

---

## 클라우드 컴퓨팅 (Cloud computing)

인터넷을 통해 IT 리소스와 애플리케이션을 온디맨드로 제공하는 서비스다.

기존의 물리적인 형태의 컴퓨팅 리소스를 네트워크 기반 서비스 형태로 제공하는 것

사용자로 하여금 네트워크 상에서 클라우드 서비스의 자원을 사용하는 것을 의미한다.

다음과 같이 3가지 분류로 나누기도 한다.

- IaaS
- PaaS
- SaaS

### IaaS (Infrastructure as a service)

- AWS, 네이버 플랫폼과 같은 인프라스트럭쳐를 제공하는 서비스
- 가상 서버 또는 스토리지, 가상 네트워크 등의 리소스를 서비스 형태로 제공한다.
- 사용자는 물리적인 하드웨어를 직접 관리할 필요가 없으며, 직접적으로 서비스 이용을 통해 컴퓨터 리소르를 사용할 수 있다. (AWS, MS 애저, IBM 소프트레이어 등의 업체)
- 클라우드 IT의 기본 구성 요소 (네트워킹, 컴퓨터, 데이터 스토리지 공간)

### PaaS (Platform as a service)

- DB 또는 Application 서버 등의 미들웨어를 제공한다.
- 하드웨어/OS/미들웨어 에 대한 관리는 서비스 제공자가 하며, 사용자는 제공된 미들웨어만 사용 할 수 있다.
- 주로 개발 환경과 관련된 서비스를 제공한다. (OS, DB, WAS, JDK)
- 기본 인프라(하드웨어나 운영체제)를 관리할 필요 없이 애플리케이션을 실행할 수 있게 해준다.

### SaaS (Software as a service)

- 소프트웨어 또는 애플리케이션의 기능만 제공한다. (네이버클라우드, 웹 메일, ERP 등과 같은 형태의 서비스를 사용자에게 제공한다.)

---

## AWS 클라우드 컴퓨팅의 장점

- 저렴한 비용

  > AWS는 사전 비용 장기 약정 없이 저렴한 종량 과금제 방식으로 운영된다.
  > 확장형 글로벌 인프라를 구축 및 관리하고, 더 저렴한 요금의 형태로 사용자에게 비용 절감 혜택을 고스란히 돌려준다.

- 속도 및 민첩성 개선

  > 데이터센터운영 및 유지관리에 비용투자 불필요
  > 빠른 배포
  > AWS는 언어 및 운영 체제에 구애받지 않는 플랫폼이다. 따라서 사용자의 비즈니스에 가장 적합한 개발 플랫폼 또는 프로그래밍 모델을 선택할 수 있다. 사용할 서비스를 한 개 또는 여러 개 선택하고, 그 사용 방식도 선택할 수 있다.

- 민첩성, 즉각적 융통성

  > 몆 주 또는 몇 개월 동안 물리적인 서버를 구축하길 기다리는 대신 즉시 새로운 앱을 배포하고, 수요를 기준으로 축소할 수도 있다. 필요한 가상 서버가 한 대든 아니면 수천 대든, 가상 서버가 필요한 시간이 몇 시간이든 사용한 양만큼 비용이 청구된다.

- 용량추정 불필요
- 데이터 센터 운영 및 유지관리 비용 불필요
- 몇 분 만에 전 세계 배포 가능

> 백엔드 서버와 관련된 모든 서비스를 제공하며 필요한 기술 또한 추가해서 사용할 수 있다.
> 또한 아마존의 모든 서비스는 API 중심으로 설계되어 있어 모든 기술이 API로 제어가 가능하다.
> 한 곳에서 필요한 모든 서비스를 찾을 수 있고, 클라우드라 확장성이 좋다보니 여러 스타트업에서 사용하고 있다.

---

## AWS 웹 호스팅

### Amazon Lightsail

간단한 웹 사이트는 일반적으로 WordPress와 같은 CMS(콘텐츠 관리 시스템), Magento와 같은 전자 상거래 애플리케이션 또는 LAMP와 같은 개발 스택을 실행하는 단일 웹 서버로 구성됩니다. 이러한 소프트웨어를 사용하면 웹 사이트의 콘텐츠를 쉽게 구축, 업데이트, 관리 및 제공할 수 있습니다.

간단한 웹 사이트는 마케팅 웹 사이트, 콘텐츠 웹 사이트 또는 블로그와 같이 작성자가 여러 명이고 자주 콘텐츠가 변경되며 트래픽이 적거나 보통인 사이트에 적합합니다. 간단한 웹 사이트는 나중에 확장될 수도 있는 웹 사이트를 위해 간단한 출발점을 제공합니다. 이러한 사이트는 보통 저렴하지만, 웹 서버의 IT 관리가 필요하며 몇 개의 서버를 초과하여 확장되거나 뛰어난 가용성을 제공하도록 설계되지 않았습니다.

다음의 사례에 가장 적합

- WordPress, Joomla, Drupal, Magento와 같은 일반적인 애플리케이션상에 구축된 웹 사이트
- LAMP, LEMP, MEAN, Node.Js와 같은 인기 있는 개발 스택상에 구축된 웹 사이트
- 서버 5개를 초과하여 확장될 가능성이 낮은 웹 사이트
- 자체적으로 웹 서버와 리소스를 관리하고자 하는 고객
- 웹 서버, DNS 및 네트워킹을 한 콘솔에서 관리하려는 고객

### AWS Amplify Console

단일 페이지 웹 앱 호스트
웹 브라우저에서 단일 로드만 필요로 하는 정적 웹 앱을 단일 페이지 웹 앱이라고 합니다. 사용자는 브라우저에 사전 로드된 HTML, JavaScript 및 CSS를 통해 모든 후속 작업을 수행할 수 있습니다. 백엔드 데이터는 페이지를 다시 로드하지 않고 데이터 스토어에서 콘텐츠를 가져오며 UI를 업데이트하는 GraphQL 또는 REST API를 통해 액세스됩니다.

단일 페이지 웹 앱은 네이티브 또는 데스크톱 앱과 같은 수준의 성능을 제공합니다. 또한 동적 기능과 놀라운 빠른 성능을 통해 낮은 비용, 높은 안정성, 서버 관리 부담 해소, 엔터프라이즈급 트래픽을 처리하기 위한 확장성 등 정적 웹사이트의 이점을 모두 제공합니다.

다음의 사례에 가장 적합

- React JS, Vue JS, Angular JS, Nuxt 등의 단일 페이지 앱 프레임워크를 사용하여 구축한 웹사이트
- Gatsby JS, React-static, Jekyll, Hugo 등의 정적 사이트 생성기를 사용하여 구축한 웹사이트
- PWA(프로그레시브 웹 앱)
- PHP 또는 ASP.NET과 같은 서버 측 스크립팅이 포함되지 않은 웹 사이트
- 서버리스 백엔드가 있는 웹사이트

### Amazon Simple Storage Service (Amazon S3)

정적 웹 사이트는 HTML, JavaScript, 이미지, 동영상 및 기타 파일을 웹 사이트 방문자에게 제공하며, PHP 또는 ASP.NET과 같은 서버 측 애플리케이션 코드를 포함하지 않습니다. 보통 개인 사이트나 마케팅 사이트를 제공하는 데 사용됩니다.

정적 웹 사이트는 비용이 매우 저렴하고, 높은 수준의 안정성을 제공하며, 서버 관리가 전혀 필요 없고, 추가 작업 없이 엔터프라이즈 수준의 트래픽을 처리하도록 확장할 수 있습니다.

다음의 사례에 가장 적합

- PHP 또는 ASP.NET과 같은 서버 측 스크립팅이 포함되지 않은 웹 사이트
- 작성자 수가 적으면 자주 변경되지 않는 웹 사이트
- 빈도는 낮지만 많은 트래픽을 수용하도록 확장되어야 하는 웹 사이트
- 인프라를 관리하지 않으려는 고객

### Amazon Elastic Cloud Computing (Amazon EC2)

엔터프라이즈 웹 사이트에는 널리 사용되는 마케팅 및 미디어 사이트와 더불어 소셜, 여행 및 기타 애플리케이션 중심의 웹 사이트가 포함됩니다. 예를 들어 Lamborghini, Coursera 및 Nordstrom에서 AWS를 사용하여 자사의 웹 사이트를 호스팅합니다. 엔터프라이즈 웹 사이트는 가장 까다롭고 트래픽이 많은 웹 사이트를 지원할 수 있도록 가용성이 뛰어나고 동적으로 리소스를 확장해야 합니다.

엔터프라이즈 웹 사이트는 여러 AWS 서비스를 사용하고 종종 여러 데이터 센터(가용 영역이라고 함)를 사용합니다. AWS상에 구축된 엔터프라이즈 웹 사이트는 높은 수준의 가용성, 확장성 및 성능을 제공하지만, 정적 또는 간단한 웹 사이트보다 많은 관리가 필요합니다.

다음의 사례에 가장 적합

- 최소한 2개의 데이터 센터에서 여러 개의 웹 서버를 사용하는 웹 사이트
- 로드 밸런싱, Auto-Scaling 또는 외부 데이터베이스를 사용하여 확장해야 하는 웹 사이트
- 지속적으로 CPU를 많이 사용해야 하는 웹 사이트
- 웹 서버 구성과 관리에 대한 최대한의 제어와 유연성이 필요한 고객

## 참고문헌

- [AWS 웹 호스팅](https://aws.amazon.com/ko/websites/?nc2=h_ql_sol_use_web)
- https://brunch.co.kr/@e9c7009de84443b/102
- https://goddaehee.tistory.com/174

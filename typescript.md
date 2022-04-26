# typescript

typescript와 함께 프로젝트 생성하는 방법
[npx create-react-app ts-react-tutorial --typescript]
프로젝트에 typescript 추가 방법
[yarn add typescript @types/node @types/react @types/react-dom @types/jest]

라우터를 사용하고자 했는데 다음과 같은 에러가 발생했다.
Module not found: Can't resolve 'react-router-dom'
다음과 같이 설치하니 해결되었다.
$ npm install react-router-dom
$ npm install @types/react-router-dom

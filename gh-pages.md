# GitHub Pages

웹 페이지를 호스팅 해주는 gh-pages 라이브러리 사용법

```bash
$ yarn add gh-pages
```

```javascript
// package.json 파일에 다음 두 가지 추가.
"homepage": "https://yty0643.github.io/portfolio",
"scripts": {
        "predeploy": "npm run build",
        "deploy": "gh-pages -d build",
    },
```

```bash
$ yarn bulid
```

해당 깃허브 저장소에서 gh-pages 설정 바꿔주면 끝.

만약 react router를 추가한 웹이라면 추가 과정 필요. 이전에 해봤지만 다음에 또 하게되면 작성하겠음.

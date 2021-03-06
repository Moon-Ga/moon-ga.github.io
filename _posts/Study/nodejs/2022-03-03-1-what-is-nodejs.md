---
title: "[Node.js] Node.js의 개념과 설치 - (1)"
categories: Node.js
---

## Node.js란?

Node.js는 구글에서 개발한 오픈 소스 자바스크립트 엔진인 크롬 V8에 비동기 이벤트 처리 라이브러리인 libuv를 결합한 플랫폼으로써, 자바스크립트로 서버를 구축하는 등 브라우저 외적인 코드를 실행할 수 있게 해준다. 내장 HTTP 서버 라이브러리를 포함하고 있기 때문에 웹 서버에서 별도의 소프트웨어 없이 동작하는 것이 가능하다. 즉, 이전까지는 자바스크립트는 프론트엔드 전용 언어로써 백엔드 측면에선 활용도가 굉장히 떨어졌으나 Node.js가 등장하면서 Server Side Application을 만들 수 있게 되는 등 이는 옛말이 되어버렸다.

## 설치 및 설치 확인

### 홈페이지에서 다운로드하여 설치

이 방법은 Node.js를 가장 간단하게 설치할 수 있지만, 웹사이트나 프로그램마다 사용하는 Node.js 버전이 다를 경우 버전 전환을 쉽게 할 수 없다는 단점이 있다. 이런 경우에는 NVM을 사용해야 한다.

1. https://nodejs.org/ 로 접속한다.
2. LTS 버전과 Current 버전 중 Current 버전은 가장 최신 버전이다 보니 실험적인 부분도 존재하고 호환성이 떨어지는 경우가 있기 때문에 LTS 버전을 선택하여 설치한다.
3. 터미널을 열어서 `node -v`를 입력했을 때, 버전이 나온다면 제대로 설치된 것이다.
4. `node`를 입력하고 엔터를 친 후, `console.log(1+1)`을 입력했을 때 2가 정상적으로 나온다면 제대로 작동하는 것이다.

### NVM을 이용하여 설치

비공식 Node.js 버전 관리자 프로그램인 NVM을 이용해 설치하는 방법으로, 상술했듯이 버전 전환이 용이하다. 단, 이는 bash가 지원되는 환경인 리눅스와 맥에서만 이용이 가능하고 Windows의 경우 NVM-Windows를 이용해야 한다. 또한 fish 사용자는 fish용 nvm을, zsh 사용자는 zsh용 플러그인을 설치해줘야 한다.

1. `$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash`  
   혹은  
   `$ wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash`  
   를 입력하여 NVM을 설치한다.
2. `$ nvm install <버전>` 으로 원하는 버전을 설치할 수 있다.
3. `$ nvm use <버전>` 으로 원하는 버전으로 전환하여 활성화 할 수 있다.

참고: [Node.js](https://nodejs.org/ko/){:target="\_blank"}

---
title: "[Node.js] 간단하게 웹 서버를 만들어 보기 - (2)"
categories: Node.js
---

## 간단한 웹 서버 만들기

Node.js를 활용하여 간단한 웹 서버를 만든 후 'Hello, World'를 출력하는 방법은 이렇다.

1. 폴더를 하나 만들고, js 파일을 생성해준다. 이제 이 파일에 웹 서버를 만들기 위한 코드를 입력할 것이다.
2. ```js
   const http = require("http");
   ```
   Node에서 사용하는 '모듈'이라고 하는 외부 자원들 중 가장 기본적인 HTTP 모듈을 로드해준다.
3. ```js
   const app = http.createServer((request, response) => {
     /* 실행할 내용 */
   });
   ```
   `createServer` 메서드로 새로운 서버를 생성한다. 이때, 콜백 함수에는 서버 요청과 서버 응답에 대한 내용을 담아준다.
4. ```js
   res.writeHead(200, {"Content-Type': 'text/plain"});
   ```
   3번에서의 `실행할 내용`에 우선`writeHead` 메서드로 응답 상태와 응답 헤더를 적어준다. 이 중에서 응답 상태는 반드시 적어줘야 한다.
5. ```js
   res.end("Hello, World");
   ```
   서버에 응답 요청이 끝났음을 알리고, 요청에 따른 응답을 요구하는 부분이다. 이 메서드는 매번 응답 요청이 발생할 때마다 반드시 적어줘야 한다.
6. ```js
   app.listen(3000);
   ```
   `3000`은 포트 번호를 의미하며 이 포트로 createServer에 대한 정보를 연결하겠다는 의미이다. 두 번째 인자로 `127.0.0.1`과 같은 호스트 네임을 제공해줘도 되지만 만약 제공하지 않을 시 `localhost`로 연결된다.

이제 주소창을 열고 `http://localhost:3000`을 입력하면 "Hello, World"가 출력되는 것을 확인할 수 있다.
하지만 이는 정말 간단한 출력일 뿐, 이를 제대로 활용하여 동적인 웹페이지를 만들기 위해선 다른 여러 요소가 병행되어야 한다. 이를 연습하기 위해 간단한 어플리케이션을 만들어 보며 공부해보자.

참고: [Node.js 공식문서](https://nodejs.org/dist/latest-v16.x/docs/api/){:target="\_blank"}

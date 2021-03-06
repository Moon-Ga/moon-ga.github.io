---
title: "[Node.js] 프로젝트로 연습해보기 - (3)"
categories: Node.js
---

## 초기 세팅

우선 연습용 프로젝트 폴더를 하나 만들고 그 안에 `index.html`, `1-first.html`, `2-second.html`, `3-thrid.html`, `main.js`를 만들어줬다.

```js
// index.html
<!DOCTYPE html>
<html>
  <head>
    <title>문가네</title>
    <meta charset="utf-8" />
  </head>
  <body>
    <h1><a href="index.html">문가네</a></h1>
    <ol>
      <li><a href="1.html">첫번째</a></li>
      <li><a href="2.html">두번째</a></li>
      <li><a href="3.html">세번째</a></li>
    </ol>
    어서오세요 문가네입니다.
  </body>
</html>
```

```js
// 1-first.html, 2-second.html, 3-third.html
// 각 페이지마다 텍스트가 조금 다를 뿐 틀 자체는 똑같게 만들어줬다.
<!DOCTYPE html>
<html>
  <head>
    <title>문가네</title>
    <meta charset="utf-8" />
  </head>
  <body>
    <h1><a href="index.html">문가네</a></h1>
    <ol>
      <li><a href="1-first.html">첫번째</a></li>
      <li><a href="2-second.html">두번째</a></li>
      <li><a href="3-third.html">세번째</a></li>
    </ol>
    첫번째 페이지입니다.
  </body>
</html>
```

다음으로, main.js로 웹 서버를 만들어줬다.

```js
// main.js
const http = require("http");
const fs = require("fs");
const app = http.createServer((req, res) => {
  if (req.url === "/") {
    req.url = "/index.html";
  }
  res.writeHead(200);
  res.end(fs.readFileSync(__dirname + req.url));
});

app.listen(3000);
```

```js
const fs = require("fs");
```

`fs`는 Node.js의 File System 모듈로, 이는 다른 파일들과 상호 작용을 가능하게 해주는 모듈이다. 이 모듈은 동기, 콜백, 프로미스 등으로 작동할 수 있다.

```js
if (req.url === "/") {
  req.url = "/index.html";
}
```

`req.url`은 `http.createServer` 메서드에서 요청을 보내는 url, 즉 Query String 부분을 의미한다. 조건문으로 req.url이 기본 주소('/')라면 `index.html`로 바꿔줌으로써 메인 페이지로 이동하도록 해줬다.

```js
res.writeHead(200);
res.end(fs.readFileSync(__dirname + req.url));
```

이후 `writeHead` 메서드로 응답 상태를 명시해줬고, `end` 메서드로 응답 요청에 대한 응답을 명시해줬다. `fs.readFileSync`은 인자로 전달되는 경로에 대한 내용을 반환하는 메서드로써, `__dirname(현재경로)+url(요청을 보내는 url)`을 설정해주었다.

이제 이 상태에서 터미널에 `node main.js`를 입력하고, `http://localhost:3000`에 접속하면 정상적으로 출력되는 것을 확인할 수 있다.

> ### `main.js`를 수정해도 화면에 반영이 안될 때
>
> 분명 `main.js`를 수정하고 화면을 새로고침 했는데 수정 사항이 반영이 안될 것이다. 왜냐하면 Node.js는 `main.js`의 변경을 자동으로 감지하여 재실행을 해주지 못하고, 사용자가 직접 재실행을 해야하기 때문이다. 그렇기에 `main.js` 파일을 수정하고 그에 대한 변경사항을 확인하고 싶다면 `CTRL + C` 를 눌러 실행을 중지하고 다시 `node main.js`를 입력해 실행해주면 된다.

> ### `favicon.ico` 관련 오류 발생 시
>
> `node main.js`를 실행했을 때, `favicon.ico`를 찾을 수 없다며 오류가 발생할 수 있다. 분명 코드 상에선 `favicon.ico`를 요청하거나 사용한다는 내용이 없음에도 불구하고, 이는 http 요청 시 자동적으로 요청되는 부분이기 때문에 발생하는 오류이다. 이를 해결하기 위해선 폴더에 `favicon.ico`라는 파일을 만들어 주면 된다. 원하는 파비콘을 넣어줘도 되고, 그냥 빈 파일만 만들어줘도 해결된다.

지금 상태에서는 각 html이 분리되어 있고, 상호 간에 연결성이 없어 굉장히 정적인 상태이다. 이제 이를 보완하여 동적으로 구현해야 한다.

참고: [Node.js 공식문서](https://nodejs.org/dist/latest-v16.x/docs/api/){:target="\_blank"}

---
title: "[Node.js] 동적인 작동 추가하기 - (5)"
categories: Node.js
---

## 공통 템플릿 만들기

현재 프로젝트 폴더에 있는 `1-first.html`, `2-second.html`, `3-third.html`은 똑같은 구조에 내용만 조금 다른 형태를 띄고 있다. 이 공통된 부분을 템플릿화 하면 각각의 html 파일을 불러와 화면에 출력해주는 것이 아닌, 현재 URL의 쿼리 파라미터에 따른 데이터를 불러와 출력하도록 수정해 볼 수 있다.

```js
// main.js
res.writeHead(200);
const template = `
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
`;
res.end(template);
```

우선 `1-first.html`에 있는 내용을 `template` 변수에 담아 출력해보았다. `a` 태그에 따라 주소가 정상적으로 변하고 있으나 내용은 당연히 `template`에 적어준 `첫번째 페이지입니다.`만 출력되고 있는 것을 확인할 수 있다. 이제 이것을 이전 글에서 익혔던 쿼리 파라미터를 활용하는 코드로 변경한다면,

```js
// main.js
const template = `
<!DOCTYPE html>
<html>
  <head>
    <title>문가네</title>
    <meta charset="utf-8" />
  </head>
  <body>
    <h1><a href="/">문가네</a></h1>
    <ol>
      <li><a href="/?id=1-first">첫번째</a></li>
      <li><a href="/?id=2-second">두번째</a></li>
      <li><a href="/?id=3-third">세번째</a></li>
    </ol>
    ${query.get("id")}
  </body>
</html>
`;
```

우선 이렇게 `a`태그의 경로를 전부 쿼리 파라미터 형식으로 바꾸어 줄 수 있다. 그리고 쿼리 파라미터에서 `id`에 해당하는 부분의 값을 가져올 수 있는 `query.get("id")`가 화면에 출력되도록 템플릿 리터럴을 사용해주면 정상적으로 작동하는 것을 확인할 수 있다. 하지만 실제로는 화면에 쿼리 파라미터에 따른 데이터가 출력이 돼야 하므로 데이터를 불러오는 코드를 만들어야 한다.

## 데이터 불러오기

데이터를 불러오는 방법은 앞서 사용했던 `fs`를 활용하면 되는데, 그 중에서도 `fs.readFile`을 사용하면 된다.

```
.
├─ data    // 폴더 생성
│  ├─ 1-first
│  ├─ 2-second
│  └─ 3-thrid
├─ 1-first.html
├─ 2-second.html
├─ 3.thrid.html
├─ favicon.ico
├─ index.html
└─ main.js
```

우선 필요한 데이터를 보관하는 `data` 폴더를 하나 만들어 준다. 그리고 `data` 폴더 안에는 각각의 html파일에 있던 본문의 내용을 작성한 파일을 넣어준다. 이 때 이 파일들은 확장자가 없는 그냥 파일이다.

```js
// main.js
res.writeHead(200);
fs.readFile(`data/${query.get("id")}`, "utf-8", (err, data) => {
  const template = `
  <!DOCTYPE html>
  <html>
    <head>
      <title>문가네</title>
      <meta charset="utf-8" />
    </head>
    <body>
      <h1><a href="/">문가네</a></h1>
      <ol>
        <li><a href="/?id=1-first">첫번째</a></li>
        <li><a href="/?id=2-second">두번째</a></li>
        <li><a href="/?id=3-third">세번째</a></li>
      </ol>
      ${data}
    </body>
  </html>
  `;
  res.end(template);
});
```

`fs.readFile` 메서드는 인자로 경로, 옵션(인코딩 등), 콜백함수를 받고 그 경로에 해당하는 파일을 불러와 콜백 함수에 있는 내용을 실행해준다. 이 코드의 경우 `data`폴더 안에 쿼리 파라미터의 id에 해당하는 이름의 파일을 불러오고, 그 파일의 내용을 `utf-8`로 인코딩을 하여, 콜백 함수로 `template`의 본문 부분에 `data`를 넣고 `res.end(template)`로 화면에 출력 해주도록 한 것이다. 이 상태로 터미널에서 `node main.js`를 실행하면 정상적으로 작동하는 것을 확인할 수 있다.

참고: [Node.js 공식문서](https://nodejs.org/dist/latest-v16.x/docs/api/){:target="\_blank"}

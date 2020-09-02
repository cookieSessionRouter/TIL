# Template Engine

### :question: Template Engine은 왜 쓰는 것일까

`response`에 담겨 있는 데이터 그 자체를 활용하거나, 해당 데이터를 가지고 어떠한 처리를 해준 후 html에 뿌려주고 싶을 때가 있을 것이다. `res.senFile`같은 경우 html을 보여줄 수 있다고 했지만, 그것은 결코 변하지 않는 정적인 페이지일 뿐이다. 로그인 이전의 사이트는 모두에게 똑같이 보여져야 하므로 `res.sendFile`만으로 충분할 수 있지만, 로그인 이후 닉네임이나 아이디와 같은 개개인 마다 다른 정보를 가지고 `'test님, 반가워요!'` 등과 같은 문구를 날려줘야 한다면 `res.sendFile`로는 불가능하다. 이렇듯, 필요한 특정 데이터를 가지고 html의 특정 부분을 조정해줘야 할 때 template engine을 사용한다.

<br>

### :rocket: Template Engine의 종류는 무엇이 있을까?

[공식 문서](https://expressjs.com/en/resources/template-engines.html)를 보니 너무 많다. 흐아; 어쩜 좋아.<br>

일단 가장 흔히들 많이 쓰는 것이 `ejs`인 것 같다. crong님이 멤버쉽 맨 처음 날 "ejs는 공부 안 해도 쉽게 사용할 수 있는데 pug는 공부좀 해봐야 한다. 이번 기회에 pug를 공부해 보자."라고 하셨던 게 기억난다.<br>

근데 공식 문서에 Guide 중 [Using template engines with Express](https://expressjs.com/en/guide/using-template-engines.html)를 보면 `pug`를 예시로 들어서 설명해줬다. 일단 pug로 진행해보자. 어찌 되었든 큰 맥락은 같을 것 같다. (`app.set`을 쓴다던가, `res.send`가 아닌 `res.render`를 해준다던가, `views` 디렉토리 하위에 템플릿들을 넣어준다던가 등등) 궁금한 것은 왜 이렇게 많은 템플릿 엔진이 있냐는 것이다. 이런 것도 찾아봐야 하는데 정말 세상에... 할 게 너무 많은 것 같다. 에휴.<br>
<br>

### template engine 사용법 (feat. pug)

1. 먼저 아래 명령어를 통해 express에게 "view engine은 pug로 쓸 거야!" 라고 알려준다.

   ```javascript
   // app.js
   ...
   app.set('view engine', 'pug');
   ...
   ```

<br>

2. 이후 아래 명령어를 통해 express에게 "views로 이용할 디렉토리는 이거야!" 라고 알려준다.<br>
   여기서 views로 사용한 디렉토리는 `__dirname`, 즉 상위 디렉토리를 모두 포함한 현재 경로이다.

   ```javascript
   // app.js
   ...
   const path = require("path");
   ...
   app.set("views", path.join(__dirname, "views"));
   ...
   ```

<br>

3. 아래 명령어를 통해 pug에 특정 내용을 뿌려준다.

   ```javascript
   app.get("/", function (req, res) {
     res.render("index", { title: "Hey", message: "Hello there!" });
   });
   ```

   - `res.send`가 아닌 `res.render`를 쓴다는 것이며, 이 또한 `res.send`와 마찬가지로 정상적인 경우 status가 `200 OK`이다.

   - `res.render` 명령어에 대한 설명
     - 첫 번째 인자 : 타겟 pug파일. 확장자 `.pug`는 생략 가능.
     - 두 번째 인자 : 타겟 데이터. 오브젝트 형태로 뿌려주게 된다.

<br>

4. 3번에서는 임의의 데이터를 뿌려줬다. 만약 post방식의 form으로부터 전달 받은 데이터를 뿌려주게 된다면?

   ```javascript
   app.post("/email_post", function (res, req) {
     res.render("email.pug", { email: req.body.email });
   });
   ```

   위와 같이 전달하고자 하는 오브젝트의 'email'이라는 key의 value로, `req.body.email`에 담겨 있는 `test@naver.com`을 전달해줄 수 있다.

# post 방식의 form 태그로부터 날라온 데이터 처리 방법

1. `get` 방식과 달리 `post` 방식은 사전에 `body-parser`라는 패키지를 하나 설치해줘야 한다.

   ```shell
   npm install body-parser --save
   ```
    > cf) get 방식은 req.param(`key`)와 같은 방식으로 이용한다고 한다.

<br>

2. `body-parser`를 사용하기 위해 메인 파일(나의 경우, `app.js`)의 상단에 아래의 코드를 적어주자.

   ```javascript
   const bodyParser = require("body-parser");
   ```

<br>

3. post 방식의 form으로부터 받아온 데이터를 처리해줄 때, 필요한 패키지 `body-parser`를 사용하겠다고 express에게 알려줘야 한다. 이것 또한 `app.use`를 이용하는데, 앞으로도 무언가를 이용해야 할 때는 이렇게 해주자.

   ```javascript
   # ...
   const express = require("express");
   # ...
   const app = express();
   # ...
   app.use(bodyParser.json()); // 1. json 형태로 넘어오는 경우
   app.use(bodyParser.urlencoded({ extended: true })); // 2. 인코딩된 url로 넘어오는 경우
   # ...
   ```
   두 경우는 그냥 무조건 그렇게 쓰이니 외워두라고 하신다 by crong.

<br>

4. app을 이용하여 post 요청을 처리하는 예시는 다음과 같다. PATH를 `/email_post`라고 가정하고 해보자.

   ```javascript
   app.post("/email_post", function (req, res) {
     console.log(req.body);
     console.log(req.body["email"]);
     res.send("<h1>Welcome, " + req.body["email"] + " !</h1>");
   });
   ```

   위 예시에서처럼 `req.body` 안에 form으로부터 넘어온 데이터가 담겨있다. 만약 내가 form 형식의 텍스트박스에 `test@naver.com`를 쳤다고 해보자. 그러면 console에 찍힌 결과는 다음과 같이 나온다.

   ```
   { email: 'test@naver.com' }
   test@naver.com
   ```

   위 결과를 통해 `req.body`는 `object`인 것을 알 수 있다. 그래서 name, 즉 `key`를 쓰라고 한 것이다. 이제 이 결과를 통해 서버 내 DB 작업을 할 수도 있고, 예시에서 `res.send`를 쓴 것과 같이 `localhost:3000/email_post` 에 `"Welcome test@naver.com !"` 을 출력해줄 수도 있다.
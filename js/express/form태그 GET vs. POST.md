# form 태그에서 GET과 POST 차이

html 파일에서 `form`태그를 이용할 때는 크게 GET방식과 POST방식을 이용한다. 사용 형태는 다음과 같다.

```html
<!-- get 방식 -->
<form action="[PATH]" method="get">
  email : <input type="text" name="email" /><br />
  <input type=submit">
</form>
```

```html
<!-- post 방식 -->
<form action="[PATH]" method="post">
  email : <input type="text" name="email" /><br />
  <input type=submit">
</form>
```

- 주의할 점은 name이 key의 역할을 해주기 때문에 꼭 넣어줘야 한다.

<br>

### GET

url에 어떠한 데이터를 붙여서

- url이 없으면 그냥 흘러 가는거고,
- 있으면 url 뒤에 `?`를 붙여서 `form` 태그를 통해 던져줄 내용들을 적어서 목적지 `PATH`에 던져준다.

<br>

단점

1. 보내줘야 하는 데이터가 url에 붙어서 가다 보니 길이에 제한이 생긴다.
2. 중요한 정보가 url을 통해 노출될 수 있다.

위와 같은 단점으로 인해 서버에 데이터를 보내줄 때는 post 방식을 이용하자.

<br>

### POST

전달하고자 하는 값이 url에 담겨져있지 않는다.

<br><br><br>

## POST 사용 예시

> test.html

```html
<form action="/email_post" method="post">
  email : <input type="text" name="email" /><br />
  <input type=submit">
</form>
```

- `PATH`를 `/email_post`로 설정했다.

<br>

> app.js

```javascript
app.post('/email_post', function(req,res) {
	# ...
});
```

<br>만약 제대로 request가 왔는지만 확인하고 싶다면 아래와 같이 적어보자.

```javascript
app.post("/email_post", function (req, res) {
  res.send("Post response is OK");
});
```
<br>

제대로 request가 온 것을 확인했다면 post 메서드를 통해 날라온 데이터를 어떻게 처리해야 하는지 살펴봐야 한다. 말이 길어지고 새롭게 md를 파도 되겠다 싶은 굵직한 내용이라 [새로운 md파일](https://github.com/Mong-Gu/TIL/blob/master/js/express/post%EB%B0%A9%EC%8B%9D%EC%9D%98%20form%20%ED%83%9C%EA%B7%B8%EB%A1%9C%EB%B6%80%ED%84%B0%20%EB%82%A0%EB%9D%BC%EC%98%A8%20%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EC%B2%98%EB%A6%AC%20%EB%B0%A9%EB%B2%95.md)을 만들었다.

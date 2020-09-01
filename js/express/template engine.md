# Template Engine

### :question: Template Engine은 왜 쓰는 것일까

`response`에 담겨 있는 데이터 그 자체를 활용하거나, 해당 데이터를 가지고 어떠한 처리를 해준 후 html에 뿌려주고 싶을 때가 있을 것이다. `res.senFile`같은 경우 html을 보여줄 수 있다고 했지만, 그것은 결코 변하지 않는 정적인 페이지일 뿐이다. 로그인 이전의 사이트는 모두에게 똑같이 보여져야 하므로 `res.sendFile`만으로 충분할 수 있지만, 로그인 이후 닉네임이나 아이디와 같은 개개인 마다 다른 정보를 가지고 `'test님, 반가워요!'` 등과 같은 문구를 날려줘야 한다면 `res.sendFile`로는 불가능하다. 이렇듯, 필요한 특정 데이터를 가지고 html의 특정 부분을 조정해줘야 할 때 template engine을 사용한다.

<br>

### :rocket: Template Engine의 종류는 무엇이 있을까?

[공식 문서](https://expressjs.com/en/resources/template-engines.html)를 보니 너무 많다. 흐아; 어쩜 좋아.<br>

일단 가장 흔히들 많이 쓰는 것이 `ejs`인 것 같다. crong님이 멤버쉽 맨 처음 날 "ejs는 공부 안 해도 쉽게 사용할 수 있는데 pug는 공부좀 해봐야 한다. 이번 기회에 pug를 공부해 보자."라고 하셨던 게 기억난다.<br>

근데 공식 문서에 Guide 중 [Using template engines with Express](https://expressjs.com/en/guide/using-template-engines.html)를 보면 `pug`를 예시로 들어서 설명해줬다. 일단 pug로 진행해보자. 어찌 되었든 큰 맥락은 같을 것 같다. (`app.set`을 쓴다던가, `res.send`가 아닌 `res.render`를 해준다던가, `views` 디렉토리 하위에 템플릿들을 넣어준다던가 등등) 궁금한 것은 왜 이렇게 많은 템플릿 엔진이 있냐는 것이다. 이런 것도 찾아봐야 하는데 정말 세상에... 할 게 너무 많은 것 같다. 에휴.<br>

이후의 내용은... 아침에 일어나서 이어서 하자. 죽을 것 같아ㅏㅏㅏ................:cry:

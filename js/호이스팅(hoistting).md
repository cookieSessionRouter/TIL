# 호이스팅(hoisting)

### 개념

호이스팅이란, 함수 안에 있는 선언들을 모두 끌어올려서 해당 함수 유효 범위의 최상단에 선언하는 것을 말한다.

- 여기서 말하는 `선언`이란, `var`/`let`/`const`를 활용한 `변수 선언`은 물론, `function`, `function *`, `class`도 포함한다.

  → 간혹 let과 const는 호이스팅이 발생하지 않는다고 하는 분들이 계신데, 그렇지 않다고 한다. `TDZ(Temporal Dead Zone)`에 대한 개념을 더 익혀 보자.

- 해당 함수의 유효 범위는 `function-scoped`와 `block-scoped`에 따라 달라진다.

<br>

### 동작 방식

1. 자바스크립트 Parser가 함수 실행 전 해당 함수를 한 번 훑고, 함수 안에 존재하는 선언에 대한 정보를 기억하고 있다가 실행시킨다.
2. 즉, 함수 내에서 아래쪽에 존재하는 내용 중 필요한 값들을 끌어올리는 것으로,
   실제로 코드가 끌어올려지는 건 아니며 자바스크립트 Parser 내부적으로 끌어올려서 처리하는 것이라 실제 메모리에서는 변화가 없다.

<br>

_reference_

1. [var, let, const 차이점](https://velog.io/@bathingape/JavaScript-var-let-const-차이점)

2. [[JavaScript] 호이스팅(Hoisting)이란](https://gmlwjd9405.github.io/2019/04/22/javascript-hoisting.html)

3. [MDN - 호이스팅](https://developer.mozilla.org/ko/docs/Glossary/Hoisting)

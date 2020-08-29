# 변수 선언 방식 (var, let, const)

JavaScript에서 변수 선언 방식은 `var`, `let`, `const` 총 세 가지 방식이 존재한다.

<br>

### 1. var

- `변수 재선언` 가능

    → 코드량이 많아 진다면, 어디에서 어떻게 사용 될지도 파악하기 힘들 뿐더러 의도와 다르게 기존의 변수에 담긴 값이 바뀔 우려가 있다.

```jsx
var weather = "Sunny";
console.log(weather);    // Sunny

var weather = "Cloudy";
console.log(weather);    // Cloudy
```

- `function-scoped`로 `hoisting` 발생

```jsx
function count() {
 for (var i = 0; i < 10; i++)
  console.log(`i = ${i}`);
 console.log(`i = ${i}`);
}

count();
// i = 0
// i = 1
// i = 2
// i = 3
// i = 4
// i = 5
// i = 6
// i = 7
// i = 8
// i = 9
// i = 10
```

- 선언되지 않은 변수에 값을 할당해줘도 `ReferenceError`이 발생하지 않음

```jsx
console.log(name);      // undefined
name = "MongGu";
console.log(name);      // MongGu
var name;
```

ES6(ES2015) 이후, 위와 같은 문제점을 해결하기 위해 `let`과 `const`가 등장했다.

<br>

### 2. let

- `변수 재선언` 불가능

    → let으로 선언된 변수는 다시 var, let, const 등을 활용하여 선언 불가능. 오직 재할당만 가능하다.

```jsx
let weather = "Sunny";
console.log(weather);

let weather = "Cloudy";     // SyntaxError: Identifier 'weather' has already been declared
console.log(weather);
```

- 재할당 가능 (`mutable`)

```jsx
let weather = "Sunny";
console.log(weather);       // Sunny

weather = "Cloudy";
console.log(weather);       // Cloudy
```

- `block-scoped`로 `hoisting` 발생

    → block-scope 단위로 hoisting이 발생하기 때문에 변수를 선언한 block 종료 시 더이상 변수는 존재하지 않음

    → 변수가 존재하지 않은 상태에서, 해당 변수에 값을 할당하거나 참조하면 `ReferenceError` 발생

```jsx
function count() {
 for (let i = 0; i < 10; i++)
  console.log(`i = ${i}`);
console.log(`i = ${i}`);
}

count();
// i = 0
// i = 1
// i = 2
// i = 3
// i = 4
// i = 5
// i = 6
// i = 7
// i = 8
// i = 9
// ReferenceError: i is not defined
```

<br>

### 3. const

- `변수 재선언` 불가능

```jsx
const weather = "Sunny";
console.log(weather);          

const weather = "Cloudy";     // SyntaxError: Identifier 'weather' has already been declared
console.log(weather);
```

- 재할당 불가능(`immutable`)

```jsx
const weather = "Sunny";
console.log(weather);         // Sunny

const weather = "Cloudy";     // TypeError: Assignment to constant variable.
console.log(weather);
```

- `block-scoped`로 `hoisting` 발생

    let과 동일한 개념이므로 생략.

<br>

### 총정리
![](./photos/var,let,const.PNG)

<br>

_reference_
1. [var, let, const 차이점은?](https://gist.github.com/LeoHeo/7c2a2a6dbcf80becaaa1e61e90091e5d)
2. [var, let, const 차이점](https://velog.io/@bathingape/JavaScript-var-let-const-차이점)

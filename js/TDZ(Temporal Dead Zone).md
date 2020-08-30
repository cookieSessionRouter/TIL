![](https://dmitripavlutin.com/static/7973b25e51eb97f6d330c941600f7ad8/55e68/temporal-dead-zone-in-javascript.webp)

위 그림과 같이 TDZ 시맨틱은 선언 전에 변수에 접근하는 것을 금지한다. 즉, 변수를 선언하기 전에는 어떤 것도 사용하는 것을 원칙으로 한다.

<br>

## 변수의 선언 단계를 통해 알아보는 TDZ

TDZ의 개념을 익히기 위해, 가벼운 변수를 예시로 생각해보자. 변수는 `선언 단계` → `초기화 단계` → `할당 단계`에 걸쳐 생성된다.

- `var`로 선언된 변수는 `선언 단계`와 `초기화 단계`가 한 번에 이루어진다.

  ```jsx
  // 스코프의 선두에서 선언 단계와 초기화 단계가 실행된다.
  // 따라서 변수 선언문 이전에 변수를 참조할 수 있다.

  console.log(foo); // undefined

  var foo;
  console.log(foo); // undefined

  foo = 1; // 할당문에서 할당 단계가 실행된다.
  console.log(foo); // 1
  ```

- `let`으로 선언된 변수는 `선언 단계`와 `초기화 단계`가 분리되어 진행된다.

  ```jsx
  // 스코프의 선두에서 선언 단계가 실행된다.
  // 아직 변수가 초기화(메모리 공간 확보와 undefined로 초기화)되지 않았다.
  // 따라서 변수 선언문 이전에 변수를 참조할 수 없다.

  console.log(foo); // ReferenceError: foo is not defined

  let foo; // 변수 선언문에서 초기화 단계가 실행된다.
  console.log(foo); // undefined

  foo = 1; // 할당문에서 할당 단계가 실행된다.
  console.log(foo); // 1
  ```

- `const`로 선언된 변수에 대해서는 단계가 어떤 식으로 진행되는지 아직 파악하지 못했다. 다만, `let`이랑 비슷하지 않을까 싶다.

  → 별개의 이야긴데, `const`로 변수를 선언할 때에는 선언과 동시에 값을 할당해줘야 함.

  ```jsx
  // let은 선언하고 나중에 값을 할당이 가능하지만
  let dd
  dd = 'test'

  // const 선언과 동시에 값을 할당 해야한다.
  const aa // Missing initializer in const declaration
  ```

<br>

변수의 생성 단계를 통해 알 수 있는 것은 다음과 같다.

1. var로 변수를 선언할 경우, 변수는 해당 스코프 내에서 `선언과 동시에 undefined로 초기화`가 된 채로 호이스팅이 진행된다. 그에 따라, 해당 스코프 내에서 var 변수를 선언한 부분이 있으면 값을 할당하기 이전에 참조를 할 수 있다.

2. let이나 const로 변수를 선언할 경우, 변수는 해당 스코프 내에서 `선언`이 된 채로 호이스팅이 진행된다. 초기화가 된 채 호이스팅이 된 것이 아니라는 것을 명심!
   해당 스코프 내에서 let이나 const로 변수를 선언한 부분이 있더라도, 값을 할당하기 이전에 값을 참조하면 초기화가 되지 않은 상태이므로 참조할 수 없다.

3. TDZ는 `선언은 됐지만 초기화는 되지 않은 변수가 들어가는 Zone`이라고 생각하면 좋다.<br>
   → 실제 소스코드 속에서 초기화를 했더라도, 초기화 이전에 변수에 담긴 값을 참조하려고 하면 `초기화되지 않은 채 호이스팅된 변수`를 참조하는거라 `참조 에러`가 발생.

<br>

## TDZ의 영향을 받는 구문

- `const` 변수

  - const 변수는 선언 및 초기화 전 줄까지 TDZ에 있다.

    ```jsx
    // Does not work!
    pi; // throws `ReferenceError`
    const pi = 3.14;
    ```

  - const 변수는 선언한 후에 사용해야 한다.

    ```jsx
    const pi = 3.14;

    // Works!
    pi; // => 3.14
    ```

<br>

- `let` 변수

  - let도 선언 전 줄까지 TDZ의 영향을 받는다.

    ```jsx
    // Does not work!
    count; // throws `ReferenceError`
    let count;

    count = 10;
    ```

  - let 변수도 선언 이후에 사용해야 한다.

    ```jsx
    let count;

    // Works!
    count; // => undefined
    count = 10;

    // Works!
    count; // => 10
    ```

<br>

- `class` 구문

  - 선언 전에는 class를 사용할 수 없다.

    ```jsx
    // Does not work!
    const myNissan = new Car("red"); // throws `ReferenceError`

    class Car {
      constructor(color) {
        this.color = color;
      }
    }
    ```

  - 클래스를 선언한 후에 사용하도록 수정한다.

    ```jsx
    class Car {
      constructor(color) {
        this.color = color;
      }
    }

    // Works!
    const myNissan = new Car("red");
    myNissan.color; // => 'red'
    ```

<br>

- `constructor()` 내부의 `super()`

  - 부모 클래스를 상속받았다면, 생성자 안에서 `super()`를 호출하기 전까지 `this 바인딩`은 TDZ에 있다.
    아래 코드를 보면, `constructor()` 안에서 `super()`가 호출되기 전까지 `this`를 사용할 수 없다.

    ```jsx
    class MuscleCar extends Car {
    constructor(color, power) {
        this.power = power;
        super(color);
    }
    }

    // Does not work!
    const myCar = new MuscleCar(‘blue’, ‘300HP’); // `ReferenceError`
    ```

  - TDZ는 인스턴스를 초기화하기 위해 부모 클래스의 생성자를 호출할 것을 제안한다. 부모 클래스의 생성자를 호출하고 인스턴스가 준비되면 자식 클래스에서 this 값을 변경할 수 있다.

    ```jsx
    class MuscleCar extends Car {
      constructor(color, power) {
        super(color);
        this.power = power;
      }
    }

    // Works!
    const myCar = new MuscleCar("blue", "300HP");
    myCar.power; // => '300HP'
    ```

<br>

- 기본 함수의 매개변수

  - 기본 매개변수는 `글로벌`과 `함수 스코프` 사이의 `중간 스코프(intermidiate scope)`에 위치한다. 기본 매개변수 또한 TDZ 제한이 있다.

    ```jsx
    const a = 2;
    function square(a = a) {
      return a * a;
    }
    // Does not work!
    square(); // throws `ReferenceError`
    ```

  - 기본 매개변수 `a`는 선언 전에 `a = a` 표현식의 오른쪽에서 사용되었다. `a`에서 참조 에러가 발생한다.
    기본 매개변수는 선언 및 초기화 다음에 사용되어야 한다. 이 경우 `init`과 같은 다른 변수로 선언하여 사용한다.

    ```jsx
    const init = 2;
    function square(a = init) {
      return a * a;
    }
    // Works!
    square(); // => 4
    ```

<br>

## TDZ의 영향을 받지 않는 구문

- `var` 변수
  <br>`var` 변수는 선언하기 전에 접근하면 `undefined`

      ```jsx
      // Works, but don't do this!
      value; // => undefined
      var value;
      ```

<br>

- `function` 구문
  <br>함수는 `var` 변수와는 다르게 선언된 위치와 상관없이 동일하게 호출됨

      ```jsx
      // Works!
      greet("World"); // => 'Hello, World!'
      function greet(who) {
          return `Hello, ${who}!`;
      }

      // Works!
      greet("Earth"); // => 'Hello, Earth!'
      ```

<br>

- `import` 모듈

  ```jsx
  // Works!
  myFunction();
  import { myFunction } from "./myModule";
  ```

<br>

## TDZ가 필요한 이유

JavaScript가 동적 언어라서 `runtime type check`가 필요해서라고 한다. 아직은 이해하기 어려운 말이다.

<br>

_reference_

1. [var, let, const 차이점은?](https://gist.github.com/LeoHeo/7c2a2a6dbcf80becaaa1e61e90091e5d)

2. [var, let, const 차이점](https://velog.io/@bathingape/JavaScript-var-let-const-차이점)

3. [TDZ을 모른 채 자바스크립트 변수를 사용하지 말라](https://ui.toast.com/weekly-pick/ko_20191014/#2-tdz%EC%9D%98-%EC%98%81%ED%96%A5%EC%9D%84-%EB%B0%9B%EB%8A%94-%EA%B5%AC%EB%AC%B8)

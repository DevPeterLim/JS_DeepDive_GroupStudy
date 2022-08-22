# 12장 함수

## 1. 함수란?

- 자바스크립트에서 가장 중요한 핵심 개념
- 수학의 함수는 입력을 받아 출력을 내보내는 일련의 과정을 정의한 것
- 프로그래밍 언어의 함수도 수학의 함수와 같은 개념

```
f(x,y) = x + y
```

```javascript
// f(x, y) = x + y
function add(x, y) {
  return x + y;
}

// f(2, 5) = 7
add(2, 5); // 7
```

- 일련의 과정을 문(`statement`)로 구현하고 코드 블록으로 감싸서 하나의 실행 단위로 정의한 것
- 함수는 아래 3가지로 이루어짐

  - 매개변수 `parameter`
  - 인수 `argument`
  - 반환값 `return value`

- 함수는 함수 정의 `function definition` 을 통해 생성됨

```javascript
// 함수 정의
function add(x, y) {
  return x + y;
}
```

- 함수는 정의만으로 실행되지 않고, 인수 `parameter`를 매개변수를 통해 함수에 전달하면서 함수의 실행을 명시적으로 지시해야 함
  - 이를 우리는 함수 호출 `function call / invoke` 라고 함

```javascript
// 함수 호출
var result = add(2, 5);

// 함수 add에 인수 2, 5를 전달하면서 호출하면 반환값 7을 반환
console.log(result); // 7
```

## 2. 함수를 사용하는 이유

- 코드의 재사용성에 유용
- 유지보수의 편의성을 높임
- 코드의 신뢰성을 높임
- 코드의 가독성을 향상

## 3. 함수 리터럴

### 리터럴?

- 리터럴은 값을 표현하는 방식

```javascript
숫자 : 3
문자 : "hello"
참 / 거짓 : true
함수 : function () {}
```

- JavaScript의 `함수는 객체 타입의 값`
- `함수 리터럴 === 함수 표현식`

```javascript
// 변수에 함수 리터럴을 할당
var f = function add(x, y) {
  return x + y;
};
```

### 함수 리터럴의 구성

- function 키워드
- 함수 이름
- 매개 변수 목록
- 함수 몸체

#### 구성요소

- 함수 이름
  - 함수 이름은 식별자
  - 함수 이름은 함수 몸체 내에서만 참조할 수 있는 식별자
  - 함수 이름은 생략 가능 (익명함수)
- 매개 변수 목록
  - 0개 이상의 매개변수를 소괄호로 감싸고 쉼표로 구분
  - 각 매개변수에는 함수를 호출할 때 지정한 인수가 순서대로 할당
  - 매개변수는 함수 몸체 내에서 변수와 동일, 식별자 네이밍 규칙을 준수해야 함
- 함수 몸체

  - 함수가 호출되었을 때 실행될 문들을 하나의 실행 단위로 정의한 코드 블록
  - 함수 호출에 의해 실행됨

- 함수 리터럴은 값을 생성하기 위한 표기법
- 함수 리터럴은 평가되어 값을 생성하고, 이 값은 객체 -> 즉 함수는 객체임
- 일반 객체는 호출할 수 없지만 함수는 호출가능

## 4. 함수 정의

- 함수 정의란?
  - 함수를 호출하기 이전에 인수를 전달받을 매개변수와 실행할 문들, 그리고 반환할 값을 지정하는 것
  - 정의된 함수는 평가되어 함수 객체가 됨

### 함수를 정의하는 4가지 방법

1. 함수 선언문

```javascript
function add(x, y) {
  return x + y;
}
```

2. 함수 표현식

```javascript
var add = function (x, y) {
  return x + y;
};
```

3. function 생성자 함수

```javascript
var add = new Function("x", "y", "x+y");
```

4. 화살표 함수 (ES6)

```javascript
var add = (x, y) => x + y;
```

### 변수 선언과 함수 정의

- 변수는 `선언` 이라고 하고, 함수는 `정의` 한다고 표현
- 함수 선언문이 평가되면 식별자가 암묵적으로 생성되고 함수 객체가 할당됨

### 4.1 함수 선언문

```javascript
// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 참조
// console.dir 은 console.log 와는 달리 함수 객체의 프로퍼티까지 출력
// 단, node.js 환경에서는 console.log와 같은 결과가 출력됨
console.dir(add); // f add (x,y)

// 함수 호출
console.log(add(2, 5)); // 7
```

- 함수 선언문은 함수 리터럴과 형태가 동일
- 함수 리터럴은 함수 이름 생략이 가능하지만 함수 선언문은 함수 이름 생략 불가
- 함수 선언문은 표현식이 아닌 `문`
- 크롬 개발자 도구의 콘솔에서 함수 선언문을 실행하면 완료값 `undefined`가 출력됨
- 함수 표현식은 표현식이 평가되어 생성된 함수가 선언됨

```javascript
function add(x, y) { return x+y;} // undefined
func = functino (x,y) { return x+y}
// f(x,y){return x+y}
```

```javascript
// 함수 선언문은 표현식이 아닌 문이므로 변수에 할당할 수 없음
// 하지만 함수 선언문이 변수에 할당되는 것처럼 보임
var add = function add(x, y) {
  return x + y;
};

// 함수 호출
console.log(add(2, 5)); // 7
```

- 위 예제는 함수 선언문을 변수에 할당하는 것처럼 보이는데, 사실 객체 리터럴 즉, 함수 표현식으로 해석
- 자바스크립트 엔진은 코드의 문맥에 따라 해석하는데, 코드블록{ }은 두가지 의미가 있는데 코드 블록일 수도 있고 객체 리터럴일 수도 있음(중의적 표현)
- { }이 값으로 평가되어야 할 문맥(예, 할당연산자의 우변)에서 피연산자로 사용되면 엔진은 { }을 객체 리터럴로 해석

- 함수 리터럴도 마찬가지로 중의적인 코드
- 함수 이름이 있는 함수 리터럴을 단독으로 사용하면(변수 할당X) 함수 선언문으로 해석하고, 함수 리터럴을 변수에 할당하거나 피연산자로 사용하면 함수 리터럴 표현식으로 해석
- 위 예제는 좌변의 변수에 할당 연산자를 통해 우변의 함수 선언문이 피연산자로 사용되면서 자바스크립트 엔진은 { }를 객체 리터럴로 해석

#### 함수 선언문과 함수 표현식(함수 리터럴) 차이

- 함수 선언문은 함수 이름 생략 불가
- JS 엔진은 함수 선언문을 해석해 함수 이름과 동일한 이름의 식별자를 암묵적으로 생성하고, 거기에 함수 객체 할당
- 함수 표현식(함수 리터럴)은 `함수 이름은 함수 몸체 내에서만 참조할 수 있는 식별자`라는 특성이 있어, 별도로 변수에 할당받지 않은 이상 호출할 수 있는 식별자가 없음

### 4.2 함수 표현식( = 함수 리터럴)

- 자바스크립트의 함수는 일급 객체
- 일급 객체는 값처럼 변수에 할당할 수 있고, 프로퍼티 값이 될 수도 있으며 배열의 요소도 될 수 있음
  - 이러한 함수의 정의방식을 `함수 표현식`이라고 함

```javascript
// 함수 표현식
var add = function (x, y) {
  return x + y;
};

console.log(add(2, 5)); //7
```

- 익명 함수: 함수 리터럴의 함수 이름을 생략한 것
- 함수 표현식의 함수 리터럴은 함수 이름을 생략하는 것이 일반적

```javascript
// 기명 함수 표현식
var add = function foo(x, y) {
  return x + y;
};

// 함수 객체를 가리키는 식별자로 호출
console.log(add(2, 5)); // 7

// 함수 이름으로 호출하면 ReferenceError가 발생한다.
// 함수 이름은 함수 몸체 내부에서만 유효한 식별자다.
console.log(foo(2, 5)); // ReferenceError: foo is not defined
```

### 4.3 함수 생성 시점과 함수 호이스팅

- 함수 선언문으로 정의한 함수는 함수 선언문 이전에 호출가능
- 함수 표현식으로 정의한 함수는 함수 표현식 이전에 호출 불가
- 함수 선은문으로 정의한 함수와 표현식으로 정의한 함수의 생성 시점이 다름

```javascript
// 함수 참조
console.dir(add); // ƒ add(x, y)
console.dir(sub); // undefined

// 함수 호출
console.log(add(2, 5)); // 7
console.log(sub(2, 5)); // TypeError: sub is not a function

// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 표현식
var sub = function (x, y) {
  return x - y;
};
```

- 함수 선언문은 런타임 이전에 함수 객체가 먼저 생성됨
- 그리고 함수 이름과 동일한 이름으로 식별자를 생성하고 생성된 함수 객체를 할당
- 즉, 코드가 실행되는 런타임시점에는 이미 함수 객체가 생성되어 있고 식별자에 할당까지 완료된 상태
- 따라서 함수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하며 이를 함수 호이스팅(function hoisting)이라고 함
  - 함수 선언문은 코드(함수 선언문을 포함한) 평가 단계에서 함수 객체 생성
  - 함수 표현식은 코드(함수 표현식을 포함한) 실행 단계에서 함수 객체 생성

#### 함수 호이스팅 vs 변수 호이스팅

- var키워드를 사용한 변수 선언문과 함수 선언문은 런타임 이전에 엔진에 의해 먼저 실행되어 식별자를 생성하는 점은 동일
- 하지만, var키워드로 선언된 변수는 undefined로 초기화되고, 함수 선언문은 함수 객체로 초기화
- var키워드를 사용한 변수는 선언문 이전에 참조하면 undefined로 평가되지만, 함수 선언문은 함수 호이스팅에 의해 호출이 가능

#### 함수 표현식

- 함수 표현식은 변수에 할당되는 값이 함수 리터럴. 즉, 문
- 변수 선언문과 할당문을 한번에 기술한 표현과 동일하게 동작
- 변수 선언은 런타임 이전에 실행되어 undefined로 초기화 되고, 변수 할당문이 실행되는 시점, 즉 런타임 시점에 함수 표현식의 함수 리터럴이 평가되어 함수 객체가 변수 할당문의 값이 되어 할당
- 결과적으로 함수 표현식은 함수 호이스팅이 발생되지 않고 변수 호이스팅만 발생

- 함수 호이스팅은 함수를 호출하기 전에 반드시 함수를 선언해야 한다는 규칙을 무시하기 때문에 함수 선언문 보다는 함수 표현식의 사용을 권장

### 4.4 Function 생성자 함수

- 자바스크립트가 기본 제공하는 빌트인 함수인 Function 생성자 함수에 매개변수 목록과 함수 몸체를 문자열로 전달하면서 new연산자와 함께 호출하면 함수 객체를 생성해서 반환
- new연산자 없이 호출해도 결과는 동일

```javascript
var add = new Function("x", "y", "return x + y");

console.log(add(2, 5)); // 7
```

- Function생성자 함수로 함수를 생성하는 방식은 권장되지 않음
- 클로저(closure)가 생성되지 않음
- 함수 선언문이나 함수 표현식으로 생성한 함수와 다르게 동작

```javascript
var add1 = (function () {
  var a = 10;
  return function (x, y) {
    return x + y + a;
  };
})();

console.log(add1(1, 2)); // 13

var add2 = (function () {
  var a = 10;
  return new Function("x", "y", "return x + y + a;"); // 클로저 환경이 만들어지지 않아 a(자유변수)를 참조할 수 없다.
})();

console.log(add2(1, 2)); // ReferenceError: a is not defined
```

### 4.5 화살표 함수

- ES6에서 도입된 화살표 함수(arrow function)는 function키워드 대신 화살표(fat arrow)=>를 사용해 간략한 방법으로 함수를 선언
- 화살표 함수는 항상 익명함수로 정의

```javascript
// 화살표 함수
const add = (x, y) => x + y;
console.log(add(2, 5)); // 7
```

- 화살표 함수는 기존의 함수보다 표현만 간략한 것이 아니라 내부 동작 또한 간략화되어 있음

1. this 바인딩 방식이 다름
2. prototype 프로퍼티가 없음
3. arguments 객체를 생성하지 않음

## 5. 함수 호출

- 함수는 함수를 가리키는 식별자와 한 쌍의 소괄호 `()` 인 함수 호출 연산자로 호출
- 함수를 호출하면 현재의 실행 흐름을 중단하고 호출된 함수로 실행 흐름을 옮김
  - 이 때 매개변수에 인수가 순서대로 할당되고 함수 몸체의 문들이 실행되기 시작함

```javascript
//함수 선언문
function add(x,y) {
  return x + y;
}

// 함수 호출
// 인수 1과 2는 매개변수 x와 y에 순서대로 할당되고 함수 몸체의 문들이 실행됨
var result - add(1, 2);
```

- 함수 매개변수의 스코프는 함수 내부임

```javascript
function add(x, y) {
  console.log(x, y); // 2 5
  return x + y;
}

add(2, 5);

// add 함수의 매개변수 x, y는 함수 몸체 내부에서만 참조할 수 있음
console.log(x, y); // ReferenceError: x is not defined
```

- 함수 매개변수의 개수와 인수의 개수가 일치하지 않아도 됨
- 인수가 부족하면 할당되지 않은 매개변수는 `undefined` 이고, 넘치는 경우 무시됨

```javascript
function add(x, y) {
  return x + y;
}

console.log(add(2)); // NaN = 2 + undefined
console.log(add(2, 3, 4)); // 5
```

- 초과되는 경우 버려지는 것은 아니고 `arguments` 객체의 프로퍼티로 보관됨

```javascript
function add(x, y) {
  console.log(arguments);
  // Arguments(3) [2, 5, 10, callee: ƒ, Symbol(Symbol.iterator): ƒ]

  return x + y;
}

add(2, 5, 10);
```

### 5.2 인수 확인

- 자바스크립트 함수는 매개변수와 인수의 개수가 일치하는지 확인하지 않음
- 자바스크립트는 동적 타입 언어
  - 따라서 자바스크립트 함수는 매개변수의 타입을 사전에 지정할 수 없음
- 위와 같은 이유로 함수를 정의할 때 적절한 인수가 전달되었는지 확인이 필요

1. `typeof` 로 확인

- 하지만 이는 런타임에서만 확인이 가능
- 그래서 타입스크립트와 같은 정적 타입을 확인할 수 있는 상위 확장 언어가 있음

```javascript
function add(x, y) {
  if (typeof x !== "number" || typeof y !== "number") {
    // 매개변수를 통해 전달된 인수의 타입이 부적절한 경우 에러를 발생시킴
    throw new TypeError("인수는 모두 숫자 값이어야 합니다.");
  }

  return x + y;
}

console.log(add(2)); // TypeError: 인수는 모두 숫자 값이어야 힘
console.log(add("a", "b")); // TypeError: 인수는 모두 숫자 값이어야 함
```

2. 단축평가를 활용해 기본값 할당하기

```javascript
function add(a, b, c) {
  a = a || 0;
  b = b || 0;
  c = c || 0;
  return a + b + c;
}

console.log(add(1, 2, 3)); // 6
console.log(add(1, 2)); // 3
console.log(add(1)); // 1
console.log(add()); // 0
```

3. ES6에 도입된 매개변수 기본값을 사용하기

```javascript
function add(a = 0, b = 0, c = 0) {
  return a + b + c;
}

console.log(add(1, 2, 3)); // 6
console.log(add(1, 2)); // 3
console.log(add(1)); // 1
console.log(add()); // 0
```

### 5.3 매개변수의 최대 개수

- ECMAScript 사양에는 매개변수의 최대 개수에 대해 명시적으로 제한하지 않음
- 가장 이상적인 매개변수의 개수는 0개
- 매개변수는 순서에 의미가 있음
- 개수가 너무 많으면 유지보수성이 나빠짐
- 최대 3개 이상을 넘지 않는 것을 권장
- 많은 매개변수가 필요하다면 객체를 활용하는 것이 유리

#### jQuery의 ajax에 객체를 인수로 전달하는 예

```javascript
$.ajax({
  method: "POST",
  url: "/user",
  data: { id: 1, name: "Lee" },
  cache: false,
});
```

- 함수 외부에서 함수 내부로 객체를 전달하는 경우 함수 내부에서 객체를 변경하면 외부의 객체가 변경되는 부수효과 side effect가 발생되니 주의!

### 5.4 반환문

- 함수는 return키워드와 표현식(반환값)으로 이뤄진 반환문을 사용해 실행 결과를 함수 외부로 반환할 수 있음

```javascript
function multiply(x, y) {
  return x * y; // 반환문
}

// 함수 호출은 반환값으로 평가됨
var result = multiply(3, 5);
console.log(result); // 15
```

- 함수 호출은 표현식
- 함수 표현식은 return키워드가 반환한 표현식의 평가 결과, 즉 반환값으로 평가됨

#### 반환문의 역할

- 함수의 실행을 중단하고 함수 몸체를 빠져나감

```javascript
function multiply(x, y) {
  return x * y; // 반환문
  // 반환문 이후에 다른 문이 존재하면 그 문은 실행되지 않고 무시됨
  console.log("실행되지 않는다.");
}

console.log(multiply(3, 5)); // 15
```

- `return` 키워드 뒤에 오는 표현식을 평가해 반환함(`return` 키워드 뒤에 표현식이 없으면 `undefined` 가 반환됨)

```javascript
function foo() {
  return;
}

console.log(foo()); // undefined
```

- 반환문은 생략할 수 있음(이때 마지막 문까지 실행 후 암묵적으로 undefined를 반환함)

```javascript
function foo() {
  // 반환문을 생략하면 암묵적으로 undefined가 반환됨
}

console.log(foo()); // undefined
```

- `return` 키워드와 표현식 사이에 줄바꿈이 잇으면 세미콜론 자동 삽입 기능으로 의도치 않은 결과가 발생할 수 있음

```javascript
function multiply(x, y) {
  // return 키워드와 반환값 사이에 줄바꿈이 있으면
  return; // 세미콜론 자동 삽입 기능(ASI)에 의해 세미콜론이 추가됨
  x * y; // 무시됨
}

console.log(multiply(3, 5)); // undefined
```

- 반환문은 함수 몸체 내부에서만 사용할 수 있음(전역에서 사용하면 문법 에러 발생)

```html
<!DOCTYPE html>
<html>
  <body>
    <script>
      return; // SyntaxError: Illegal return statement
    </script>
  </body>
</html>
```

## 6. 참조에 의한 전달과 외부 상태의 변경

- 원시 값과 객체의 비교’에서 살펴 봤듯이
  - 원시값은 값에 의한 전달(pass by value),
  - 객체는 참조에 의한 전달(pass by reference)방식으로 동작
- 함수의 매개변수도 동일

```javascript
// 매개변수 primitive는 원시값을 전달받고, 매개변수 obj는 객체를 전달받는다.
function changeVal(primitive, obj) {
  primitive += 100;
  obj.name = "Kim";
}

// 외부 상태
var num = 100;
var person = { name: "Lee" };

console.log(num); // 100
console.log(person); // {name: "Lee"}

// 원시값은 값 자체가 복사되어 전달되고 객체는 참조값이 복사되어 전달됨
changeVal(num, person);

// 원시값은 원본이 훼손되지 않음
console.log(num); // 100

// 객체는 원본이 훼손됨
console.log(person); // {name: "Kim"}
```

- 위 예제와 같이 person객체를 매개변수로 전달하면 함수 내부에서 이를 수정할 경우 원본 객체가 변경되는 부수 효과(side effect)가 발생함
- 원시값은 값을 복사해 전달하기 때문에 영향 없음

#### 순수 함수란

- 외부의 상태를 변경하지 않고, 외부 상태에 의존하지도 않는 함수
- 함수가 외부 상태를 변경하게 되면 상태 변화를 추적하기 어려워짐
- 이는 코드의 복잡성을 증가시키고 가독성을 해치는 원인이 됨
- 순수 함수를 통해 부수효과를 최대한 억제하여 오류를 피하고 안정성을 높이는 패러다임을 함수형 프로그래밍이라 함

## 7. 다양한 함수의 형태

### 7.1 즉시 실행 함수

- 함수의 정의와 동시에 즉시 호출되는 함수(IIFE Immediately Invoked Function Expression)
- 단 한 번만 호출되며 다시 호출할 수 없음

```javascript
// 익명 즉시 실행 함수
(function () {
  var a = 3;
  var b = 5;
  return a * b;
})();
```

- 익명함수를 사용하는 것이 일반적
- 기명함수도 사용할 수 있음
- 그룹연산자()내의 기명함수는 함수 선언문이 아니라 함수 리터럴로 평가되며 함수 이름은 함수 몸체에서만 참조가능하여 호출할 수 없음

```javascript
// 기명 즉시 실행 함수
(function foo() {
  var a = 3;
  var b = 5;
  return a * b;
})();

foo(); // ReferenceError: foo is not defined
```

- 즉시 실행 함수는 반드시 그룹 연산자 ()로 감싸야 함

```javascript
function () { // SyntaxError: Function statements require a function name
  // ...
}();
```

- 함수 선언문의 형식이 맞지 않는다. 함수 선언문은 함수 이름을 생략할 수 없음
- 그렇다면 기명함수를 정의해 호출해 봐도 에러가 남

```javascript
function foo() {
  // ...
}(); // SyntaxError: Unexpected token ')'
```

- 이유는 세미콜론 자동 삽입 기능 때문인데, 선언문이 끝나는 위치 코드 블럭의 닫는 중괄호 }뒤에 ;세미콜론이 삽입되어 에러가 남

```javascript
function foo() {}(); // => function foo() {};();
```

- 그룹 연산자()만 작성하면 피연산자가 없기 때문에 에러가 남

```javascript
(); // SyntaxError: Unexpected token )
```

- 무명이든 기명이든 함수를 그룹 연산자()로 감싸면 함수 리터럴로 평가되어 함수 객체가 됨

```javascript
console.log(typeof function f() {}); // function
console.log(typeof function () {}); // function
```

#### ※ 그룹 연산자 이외의 연산자 사용

```javascript
(function () {
  // ...
})();

(function () {
  // ...
})();

!(function () {
  // ...
})();

+(function () {
  // ...
})();
```

- 즉시 실행 함수도 일반 함수처럼 값을 반환하고 인수도 전달

```javascript
// 즉시 실행 함수도 일반 함수처럼 값을 반환할 수 있다.
var res = (function () {
  var a = 3;
  var b = 5;
  return a * b;
})();

console.log(res); // 15

// 즉시 실행 함수에도 일반 함수처럼 인수를 전달할 수 있다.
res = (function (a, b) {
  return a * b;
})(3, 5);

console.log(res); // 15
```

### 7.2 재귀 함수

- 함수 자기 자신을 호출하는 것을 재귀 호출(recursive call)이라 함

```javascript
function countdown(n) {
  if (n < 0) return;
  console.log(n);
  countdown(n - 1); // 재귀 호출
}

countdown(10);
```

```javascript
// 함수 표현식
var factorial = function foo(n) {
  // 탈출 조건: n이 1 이하일 때 재귀 호출을 멈춤
  if (n <= 1) return 1;
  // 함수를 가리키는 식별자로 자기 자신을 재귀 호출
  return n * factorial(n - 1);

  // 함수 이름으로 자기 자신을 재귀 호출할 수도 있음
  // console.log(factorial === foo); // true
  // return n * foo(n - 1);
};

console.log(factorial(5)); // 5! = 5 * 4 * 3 * 2 * 1 = 120
```

- 함수 식별자는 `factorial`이지만 함수 내부에서는 함수 이름 `foo`를 사용해 호출할 수 있음
- 당연히 함수 식별자 `factorial`로도 함수 내부에서 호출 가능

### 7.3 중첩 함수

- 중첩 함수(nested function)또는 내부 함수(inner function)라 함
- 그리고 중첩 함수를 포함하는 함수는 외부 함수(outer function)라 함

```javascript
function outer() {
  var x = 1;

  // 중첩 함수
  function inner() {
    var y = 2;
    // 외부 함수의 변수를 참조할 수 있음
    console.log(x + y); // 3
  }

  inner();
}

outer();
```

- ES6부터는 함수 선언문을 if문이나 for문 등의 코드 블록 내에서도 정의할 수 있음
- 단, 호이스팅으로 인해 혼란이 발생할 수 있으므로 바람직하지 않음
- 중첩 함수는 클로저와 관련이 있음

### 7.4 콜백 함수

- 함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수를 콜백 함수(`callback function`)라고 함
- 매개변수를 통해 함수의 외부에서 콜백 함수를 전달받은 함수를 고차 함수(`Higher-Order Function, HOF`)라고 함

```javascript
// n만큼 어떤 일을 반복
function repeat(n) {
  // i를 출력
  for (var i = 0; i < n; i++) console.log(i);
}

repeat(5); // 0 1 2 3 4
```

- 위 예제를 아래와 같이 변경하여 공통적으로 수행하는 일을 미리 정의해 재사용할 수 있음

```javascript
// 외부에서 전달받은 f를 n만큼 반복 호출
function repeat(n, f) {
  for (var i = 0; i < n; i++) {
    f(i); // i를 전달하면서 f를 호출
  }
}

var logAll = function (i) {
  console.log(i);
};

// 반복 호출할 함수를 인수로 전달
repeat(5, logAll); // 0 1 2 3 4

var logOdds = function (i) {
  if (i % 2) console.log(i);
};

// 반복 호출할 함수를 인수로 전달
repeat(5, logOdds); // 1 3
```

#### ※고차 함수

- 콜백 함수를 전달받은 함수
- 콜백 함수를 자신의 일부분으로 합성
- 전달받은 콜백함수의 호출 시점을 결정해서 호출
- 콜백 함수에 인수를 전달할 수 있음

- 익명함수 리터럴로 정의하면서 곧바로 고차 함수에 전달하는 것이 일반적

```javascript
// 익명 함수 리터럴을 콜백 함수로 고차 함수에 전달
// 익명 함수 리터럴은 repeat 함수를 호출할 때마다 평가되어 함수 객체를 생성
repeat(5, function (i) {
  if (i % 2) console.log(i);
}); // 1 3
```

- 함수형 프로그래밍 패러다임뿐만 아니라 비동기 처리(이벤트, Ajax통신, 타이머함수 등)에 활용되는 중요한 패턴

```javascript
// 콜백 함수를 사용한 이벤트 처리
// myButton 버튼을 클릭하면 콜백 함수를 실행
document.getElementById("myButton").addEventListener("click", function () {
  console.log("button clicked!");
});

// 콜백 함수를 사용한 비동기 처리
// 1초 후에 메시지를 출력
setTimeout(function () {
  console.log("1초 경과");
}, 1000);
```

- 모든 콜백 함수가 고차 함수에 의해 호출되는 것은 아님
- setTimeout함수의 콜백 함수는 setTimeout함수가 호출하지 않음

#### 배열 고차 함수

```javascript
// 콜백 함수를 사용하는 고차 함수 map
var res = [1, 2, 3].map(function (item) {
  return item * 2;
});

console.log(res); // [2, 4, 6]

// 콜백 함수를 사용하는 고차 함수 filter
res = [1, 2, 3].filter(function (item) {
  return item % 2;
});

console.log(res); // [1, 3]

// 콜백 함수를 사용하는 고차 함수 reduce
res = [1, 2, 3].reduce(function (acc, cur) {
  return acc + cur;
}, 0);

console.log(res); // 6
```

### 7.5 순수 함수와 비순수 함수

#### 순수 함수

```javascript
var count = 0; // 현재 카운트를 나타내는 상태

// 순수 함수 increase는 동일한 인수가 전달되면 언제나 동일한 값을 반환
function increase(n) {
  return ++n;
}

// 순수 함수가 반환한 결과값을 변수에 재할당해서 상태를 변경
count = increase(count);
console.log(count); // 1

count = increase(count);
console.log(count); // 2
```

- 외부 상태에 의존하지 않고 변경하지도 않는, 부수효과가 없는 함수
- 동일한 인수가 전달되면 언제나 동일한 값을 반환
- 전달된 인수에게만 의존해 반환값을 생성

#### 비순수 함수

```javascript
var count = 0; // 현재 카운트를 나타내는 상태: increase 함수에 의해 변화

// 비순수 함수
function increase() {
  return ++count; // 외부 상태에 의존하며 외부 상태를 변경
}

// 비순수 함수는 외부 상태(count)를 변경하므로 상태 변화를 추적하기 어려워짐
increase();
console.log(count); // 1

increase();
console.log(count); // 2
```

- 외부 상태에 의존하거나 외부 상태를 변경하는, 부수효과가 있는 함수
- 외부상태에 따라 반환값이 달라짐

- 매개변수를 통해 객체를 전달받으면 비순수 함수가 됨
- 순수 함수를 사용하는 것이 좋음
- 함수형 프로그래밍은 외부 상태를 변경하는 부수효과를 최소화해서 불변성(immutable)을 지향하는 프로그래밍 패러다임
- 함수형 프로그래밍은 순수 함수를 통해 부수 효과를 최대한 억제하여 오류를 피하고, 프로그램의 안정성을 높이는 노력의 일환

## this

this 는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수다.</br>
this 를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.

```
// 객체 리터럴
const circle = {
 radius: 5,
 getDiameter() {
 // this는 메서드를 호출한 객체를 가리킨다.
 return 2 * this.radius;
 }
};
console.log(circle.getDiameter()); // 10
```

```
/ 생성자 함수
function Circle(radius) {
 // this는 생성자 함수가 생성할 인스턴스를 가리킨다.
 this.radius = radius;
}
Circle.prototype.getDiameter = function () {
 // this는 생성자 함수가 생성할 인스턴스를 가리킨다.
 return 2 * this.radius;
};
// 인스턴스 생성
const circle = new Circle(5);
console.log(circle.getDiameter()); // 10
```

자바스크립의 this는 함수가 호출되는 방식에 따라 this에 바인딩될 값, 즉 this 바인딩이 동적으로 결정된다.

```
// this는 어디서든지 참조 가능하다.
// 전역에서 this는 전역 객체 window를 가리킨다.
console.log(this); // window
function square(number) {
 // 일반 함수 내부에서 this는 전역 객체 window를 가리킨다.
 console.log(this); // window
 return number * number;
}
square(2);
const person = {
 name: 'Lee',
 getName() {
 // 메서드 내부에서 this는 메서드를 호출한 객체를 가리킨다.
 console.log(this); // {name: "Lee", getName: ƒ}
 return this.name;
 }
};
console.log(person.getName()); // Lee
function Person(name) {
 this.name = name;
 // 생성자 함수 내부에서 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
 console.log(this); // Person {name: "Lee"}
}
const me = new Person('Lee');
```

strict mode :  https://beomy.tistory.com/13


### 함수 호출 방식

1. 일반 함수 호출
2. 메서드 호출
3. 생성자 함수 호출
4. Function.prototype.apply/call/bind 메서드에 의한 간접 호출

```
// this 바인딩은 함수 호출 방식에 따라 동적으로 결정된다.
const foo = function () {
 console.dir(this);
};
// 동일한 함수도 다양한 방식으로 호출할 수 있다.
// 1. 일반 함수 호출
// foo 함수를 일반적인 방식으로 호출
// foo 함수 내부의 this는 전역 객체 window를 가리킨다.
foo(); // window
// 2. 메서드 호출
// foo 함수를 프로퍼티 값으로 할당하여 호출
// foo 함수 내부의 this는 메서드를 호출한 객체 obj를 가리킨다.
const obj = { foo };
obj.foo(); // obj
// 3. 생성자 함수 호출
// foo 함수를 new 연산자와 함께 생성자 함수로 호출
// foo 함수 내부의 this는 생성자 함수가 생성한 인스턴스를 가리킨다.
new foo(); // foo {}
// 4. Function.prototype.apply/call/bind 메서드에 의한 간접 호출
// foo 함수 내부의 this는 인수에 의해 결정된다.
const bar = { name: 'bar' };
foo.call(bar); // bar
foo.apply(bar); // bar
foo.bind(bar)(); // bar
```

#### 일반 함수 호출

기본적으로 this에는 전역 객체global object가 바인딩된다. 

```
function foo() {
 console.log("foo's this: ", this); // window
 function bar() {
 console.log("bar's this: ", this); // window
 }
 bar();
}
foo();
```
 전역 함수는 물론이고 중첩 함수를 일반 함수로 호출하면 함수 내부의 this에는 전역 객체가 바인딩된다.
 this 는 객체의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수. 
 객체를 생성하지 않는 일반 함수의 this 는 의미가 없다.
 메서드 내에서 정의한 중첩함수도 , 콜백함수도 일반함수로 호출시 this에는 전역 객체가 바인딩 된다.
 
 ##### 일반함수 호출 시 전역 객체가 아닌 메서드의 this바인딩과 일치시키는 법<br/><br/>
 
 불일치
 ```
 var value = 1;
 const obj = {
 value: 100,
 foo() {
  console.log("foo's this: ", this); // {value: 100, foo: ƒ}
  // 콜백 함수 내부의 this에는 전역 객체가 바인딩된다.
  setTimeout(function () {
   console.log("callback's this: ", this); // window
   console.log("callback's this.value: ", this.value); // 1
  }, 100);
 }
};
obj.foo();
 ```
 
일치 : that에 this 를 할당
```
var value = 1;
const obj = {
 value: 100,
 foo() {
 // this 바인딩(obj)을 변수 that에 할당한다.
 const that = this;
 // 콜백 함수 내부에서 this 대신 that을 참조한다.
 setTimeout(function () {
  console.log(that.value); // 100
 }, 100);
 }
};
obj.foo();
 ```
 일치 : 화살표 함수를 사용
 ```
 var value = 1;
const obj = {
 value: 100,
 foo() {
 // 화살표 함수 내부의 this는 상위 스코프의 this를 가리킨다.
 setTimeout(() => console.log(this.value), 100); // 100
 }
};
obj.foo();
```

일치 : 프로토 타입을 이용하기(unction.prototype.apply, Function.prototype.call, Function.prototype.bind)
```
var value = 1;
const obj = {
 value: 100,
 foo() {
 // 콜백 함수에 명시적으로 this를 바인딩한다.
 setTimeout(function () {
 console.log(this.value); // 100
 }.bind(this), 100);
 }
};
obj.foo();
```

 
 
 
 #### 메서드 호출
 
 메서드 내부의 this는 메서드를 소유한 객체가 아닌 메서드를 호출한 객체에 바인딩된다는 것을 유의하자

 ```
 const person = {
 name: 'Lee',
 getName() {
 // 메서드 내부의 this는 메서드를 호출한 객체에 바인딩된다.
 return this.name;
 }
};
// 메서드 getName을 호출한 객체는 person이다.
console.log(person.getName()); // Lee
```
<img width="517" alt="image" src="https://user-images.githubusercontent.com/105151560/184317427-08976291-02f7-4ca8-979d-91ae705908b4.png">
프로토타입 메서드 내부에서 사용된 this도 일반 메서드와 마찬가지로 해당 메서드를 호출한 객체에 바인딩 된다.


#### 생성자 함수 호출
생성자 함수 내부의 this에는 생성자 함수가 (미래에) 생성할 인스턴스가 바인딩된다.
```
// 생성자 함수
function Circle(radius) {
 // 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
 this.radius = radius;
 this.getDiameter = function () {
 return 2 * this.radius;
 };
}
// 반지름이 5인 Circle 객체를 생성
const circle1 = new Circle(5);
// 반지름이 10인 Circle 객체를 생성
const circle2 = new Circle(10);
console.log(circle1.getDiameter()); // 10
console.log(circle2.getDiameter()); // 20
```





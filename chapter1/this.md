# this란?

    this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수이다.
    this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.

## this는 쓰이는 상황에 따라 바인딩되는 값이 변한다.

    this는 쓰이는 상황에 따라, 좀 더 구체적으로 호출되는 시점에 바인딩되는 값이 정해진다.

    1. 일반 함수로 호출할 경우 this는 전역객체를 가르킨다.
    2. 생성자 함수로 호출할 경우 this는 생성될 객체를 가르킨다.
    3. 객체 내에서 사용될 경우 메소드가 속한 객체를 가르킨다.

```js
function foo() {
  console.log(this);
}

// 1.
foo(); // 전역 객체인 window를 가르킨다.

// 2.
new foo(); // 생성될 객체를 가르킨다. foo {}

// 3.
const obj = { foo };
obj.foo(); // 메소드가 속한 객체를 가르킨다. {foo: f}
```

## Function.prototype.call, apply, bind

    this가 호출되는 시점에 바인딩되는 값이 정해진다면 개발자가 의도치 않은 값이
    바인딩될 가능성이 있다. 이러한 문제를 해결하기 위해 빌트인 객체 Function의 프로토타입에서
    call, apply, bind와 같은 함수를 제공한다.

```js
function foo(a = 0, b = 0) {
  console.log(this.value, a, b);
}

const obj = { value: 3 };

// apply의 경우 첫번째 인자로 this가 바인딩 될 값을 받고
// 두번째 인자로 함수의 매개변수로 전달될 값을 arr로 받는다.
// 그리고 함수를 실행한다.
console.log(foo.apply(obj, [1, 2]));
// 3 1 2

// call의 경우 첫번째 인자로 this가 바인딩 될 값을 받고
// 두번째 인자부터 함수의 매개변수로 전달될 값을 받는다.
// 그리고 함수를 실행한다.
console.log(foo.call(obj, 1, 2));
// 3 1 2

// bind의 경우 인자로 this가 바인딩 될 값을 받는다.
// 그리고 this가 바인딩 된 함수를 반환한다.
foo.bind(obj)(1, 2);
// 3 1 2
```

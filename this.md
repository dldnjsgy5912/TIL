> this 는 함수(메소드)를 호출한 객체를 가르킨다.

즉 this 는 자신의 위치에서 상위에 있는 객체를 가르키는것이다.

#### 기본바인딩

```js
console.log(this); // window
```

```js
function test() {
  console.log(this); // window
}
```

#### 암시적 바인딩

```js
const test = {
	name:"test"
    fun:function test () {
     console.log(this) // {name:"test",fun:f}
    }
}
```

#### 명시적 바인딩

```js
function foo() {
    console.log(this.a);
}

const obj = { a: 1 };

foo.call(obj); // 1

-------------------------------

function add(a, b) {
    return a + b;
}

add.call(null, 1, 2); // 3
add.apply(null, [1, 2]); // 3
```

#### new 바인딩

```js
function Foo() {
  console.log(this);
}

new Foo(); // Foo
```

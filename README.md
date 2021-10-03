### 자바스크립트 (Javascript)
- 자바스크립트는 개발자가 별도의 컴파일 작업을 수행하지 않는 인터프리터 언어(Interpreter language)이다. 
대부분의 모던 자바스크립트 엔진(Chrome의 V8, FireFox의 Spidermonkey, Safari의 JavaScriptCore, 
Microsoft Edge의 Chakra 등)은 인터프리터와 컴파일러의 장점을 결합하여 비교적 처리 속도가 느린 인터프리터의 단점을 해결했다. 
인터프리터는 소스코드를 즉시 실행하고 컴파일러는 빠르게 동작하는 머신 코드를 생성하고 최적화한다.

### 인터프리터 & 컴파일러
- Runtime
> 어떤 프로그램이 실행되는 동안의 시간

- 컴파일(Compile)
> 프로그래밍 언어를 Runtime 이전에 기계어로 해석하는 작업 방식이다.

- 인터프리터(Interpreter)
> 런타임 이후에 Row 단위로 해석(Interpret) 하며 프로그램을 구동시키는 방식이다.

- 수행 속도
> 컴파일러 > 인터프리터

- 리터럴(literal)
> 소스코드 안에서 직접 만들어 낸 상수 값 자체를 말하며 값을 구성하는 최소 단위

### 호이스팅 (hoisting)
- 스코프 내부 어디서든 변수 선언은 최상위에 선언된 것 처럼 행동
- 자바스크립트는 ES6의 let, const를 포함하여 모든 선언(var, let, const, function, function*, class)을 호이스팅(Hoisting)한다.   

### 변수의 생성과정
- 선언단계 > 초기화 단계 > 할당 단계
  - var : 선언과 초기화가 동시에 된다.
  - let : 선언과 초기화가 분리되어 된다.
  - const : 선언, 초기화, 할당이 동시에 되어야한다.

### var : 함수 스코프 (function-scoped)
- 함수 내에서 선언된 변수는 그 지역변수가 된다.
### let, const : 블록 스코프 (block-scoped)
- 코드블록내에서만 유효하며, 외부에서는 접근이 안된다.

### 생성자 함수 (생성자 함수명은 첫문자를 대문자로 기술하여 혼란을 방지함)
```js
 function Person(name, gender) {
	this.name = name;				//프로퍼티
	this.gender = gender;			//프로퍼티
	this.sayHello = function() {	//메소드
	    console.log('Hi, My name is ' + this.name);
	  }
	}

  let person1 = new Person('Harry', 'male')
```

### 객체 메소드
- Object.assign() : 객체 복제
```js
 const user = {
	 name: 'Harry',
	 age: 36
 }

 const newUser = Object.assign({}, user);
 // {name: 'Harry', age: 36}
 // const newUser = user -> 같은 메모리 주소라 newUser에서 값을 변경하면 user의 값도 변경됨.
```
- Object.keys() : 키 배열 반환
```js
 const user = {
	 name: 'Harry',
	 age: 36
 }

 Object.keys(user); // ['name', 'age']
```
- Object.values() : 값 배열 반환
```js
 const user = {
	 name: 'Harry',
	 age: 36
 }

 Object.values(user); // ['Harry', 36]
```
- Object.entries() : 키/값 배열 반환
```js
 const user = {
	 name: 'Harry',
	 age: 36
 }

 Object.entries(user); // ['name', 'Harry']['age', 36]
```
- Object.fromEntries() : 키/값 배열을 객체로
```js
 const arr = [
	 ["name", "Harry"],
	 ["age", 36],
	 ["gender", "male"]
 ];
 
 Object.fromEntries(arr); 
 // { age: 36, gender: "male", name: Harry" }
```

### 숫자, 수학
- toString(radix)
- radix 수의 값을 나타내기 위해 사용되기 위한 기준을 정하는 2와 36사이의 정수. (진수를 나타내는 기수의 값.)
- 숫자 10을 2진수/16진수 문자열로 바꿀경우
```js
let num = 10;
num.toString(2); // '1010'

let num2 = 255;
num2.toString(16) // 'ff'
```

### 배열 메소드
- arr.map(fn) : 함수를 받아 특정 기능을 시행하고 새로운 배열을 반환
- arr.sort() : 배열 재정렬
```js
let arr = [27, 8, 5, 13];

arr.sort(); // [13, 27, 5, 8] : 정렬할 때 요소를 문자열로 취급
```
```js
let arr = [27, 8, 5, 13];

function fn(a, b) {
	return a-b;
}
arr.sort(fn); // [5, 8, 13, 27]
// 두 요소를 전달하고 양수, 음수, 0 인지 확인한다.
// 작은 값이 앞으로 온다
```
- arr.reduce() : 인수로 함수를 받음 (누적값, 현재값) => {return 계산값};
```js
let userList = [
  { name: "Mike", age: 30 },
  { name: "Tom", age: 10 },
  { name: "Jane", age: 32 },
  { name: "Harry", age: 36 },
  { name: "Gabbie", age: 22 },
]

const result = userList.reduce((prev, cur) => {
  if (cur.age > 19) {
    prev.push(cur.name);
  }
  return prev;
}, []);
//['Mike', 'Jane', 'Harry', 'Gabbie']
```

### 나머지 매개변수, 전개 구문
- es6 를 사용하는 환경이라면 나머지 매개변수를 사용
```js
// 나머지 매개변수, 전달 받은 모든 수를 더해야함
function showName(...names) {
   console.log(names);
}

showName(); 							// []
showName('Mike');					// ['Mike']
showName('Mike', 'Tom');	// ['Mike', 'Tom']
```
- 전개 구문
```js
let user = { name: "Harry" };
let info = { age: 30 };
let fe = [ "JS", "C#", "React" ];
let lang = ["Korean", "English"];

user = {
  ...user,
  ...info,
  skills: [
    ...fe,
    ...lang
  ]	
};
// age: 30
// name: "Harry"
// skills: (5) ['JS', 'C#', 'React', 'Korean', 'English']
```

### 클로저(Closure)
- 자바스크립트는 어휘적 환경(Lexical Environment)을 갖는다.
- 함수와 렉시컬 환경의 조합
- 함수가 생성될 당시의 외부 변수를 기억 생성 이후에도 계속 접근 가능
```js
function makeCounter() {
  let num = 0;		// 은닉화
  
  return function () {
    return num++;
  }
}

let counter = makeCounter();

console.log(counter());	// 0
console.log(counter());	// 1
console.log(counter());	// 2
```

### call, apply, bind
- 함수 호출 방식과 관계없이 this를 지정할 수 있음.
- call : 모든 함수에서 사용할 수 있으며, this를 특정값으로 지정 가능.
```js
const harry = {
	name: "Harry",
};

function update(birthYear, occupation) {
	this.birthYear = birthYear;
	this.occupation = occupation;
}

update.call(harry, 1986, "developer");

console.log(harry);
/*
{
	birthYear: 1986,
	name: "Harry",
	occupation: "developer"
}
/*
```

- apply : call은 일반적인 함수와 마찬가지로 매개변수를 직접 받지만, apply는 매개변수를 배열로 받음.
```js
const harry = {
	name: "Harry",
};

function update(birthYear, occupation) {
	this.birthYear = birthYear;
	this.occupation = occupation;
}

update.apply(harry, [1986, "developer"]);

console.log(harry);
/*
{
	birthYear: 1986,
	name: "Harry",
	occupation: "developer"
}
/*
```

- bind : 함수의 this 값을 영구히 바꿈
```js
const harry = {
	name: "Harry",
};

function update(birthYear, occupation) {
	this.birthYear = birthYear;
	this.occupation = occupation;
}

const updateHarry = update.bind(harry)
updateHarry(1986, "developer");
console.log(harry);
/*
{
	birthYear: 1986,
	name: "Harry",
	occupation: "developer"
}
/*
```

### 상속, 프로토타입
```js
const car = {
 wheels: 4,
 drive() {
	 consoel.log("drive..");
 },
};

const bmw = {
	color: "grey",
	navigation: 1,
};

bmw.__proto__ = car;

const x5 = {
	color: "white",
	name: "x5",
};

x5.__proto__ = bmw;
/*
x5 는 bmw, car를 상속받음. (프로토 타입 체인)

color: "white"
name: "x5"
[[Prototype]]: Object
	color: "grey"
	navigation: 1
		[[Prototype]]: Object
			drive: ƒ drive()
			wheels: 4
*/
```

### 클래스
- ES6 에 추가된 스펙
- class 키워드 사용
- constructor 는 객체를 만들어주는 생성자 메서드
- showName은 User2 에 프로토 타입에 저장됨
```js
class User2 {
	constructor(name, age) {
		this.name = name;
		this.age = age;		
	}
	showName() {
		console.log(this.name);
	}
}

const tom = new User2("Tom", "26");
// tom 
// User2 {name: 'Tom', age: '26'}
```

- class 를 상속받을때는 extends 키워드 사용
- 메소드 오버라이딩을 사용은 super 키워드 사용
```js
class Car {
	constructor(color) {
		this.color = color;
		this.wheels = 4;
	}
	drive() {
		console.log("drive..");		
	}
	stop() {
		console.log("stop..");				
	}
}

class Bmw extends Car {
	part() {
		console.log("PARK");
	}
	stop() {
		super.stop();
		console.log("OFF");
	}
}

const z4 = new Bmw("blue");
// z4.drive() -> drive..
// z4.stop() -> stop.. -> OFF
```

### 프로미스(Promise)
- 콜백함수 : 어떤일이 완료되고 실행되는 함수
```js
const pr = new Promise((resolve, reject) => {
	// resolve : 성공
	// reject: 실패
});

Promise.all([배열]).then((res) => {
	// 동작
});
```

### async, await
- 함수 앞에 async 키워드를 사용하면 promise를 반환한다
- 함수를 호출하고 then 을 사용할 수 있다.
```js
async function getName() {
  return "Mike";
}

console.log(getName());
// [[Prototype]]: Promise
// [[PromiseState]]: "fulfilled"
// [[PromiseResult]]: "Mike"

getName().then((name) => {
	console.log(name);
})
```

- await 키워드는 async 함수 내부에서만 사용 가능
```js
function getName(name) {
	return new Promise((resolve, reject) => {
		setTimeout(() => {
			resolve(name);			
		}, 1000);
	});
}

async function showName() {
	const result = await getName("Mike");
	console.log(result);
}

showName();
```

### generator
- 함수의 실행을 중간에 멈췄다가 재개할 수 있는 기능
- function 옆에 * 를 사용하고 yield 로 함수의 실행을 멈춘다.
- generator 객체는 next 메소드가 있다.
- next 메소드 사용하면 가장 가까운 yield 를 만날때까지 실행
- 반환된 데이터 객체는 value, done 프로퍼티를 가진다.
```js
function* fn() {
	try {
		console.log(1);
		yield 1;
		console.log(2);
		yield 2;
		console.log(3);
		console.log(4);
		yield 3;
		return "finish"
	} catch (e) {
		console.log(e);
	}
}

const a = fn();
```
- Symbol.iterator 메서드가 있다.
- Symbol.iterator 는 iterator 를 반환해야 한다.
- 작업이 끝나면 done 은 true 가 된다.
```js
const arr = [1, 2, 3, 4, 5];

const it = arr[Symbol.iterator]();

it.next(); // {value: 1, done: false}
it.next(); // {value: 2, done: false}
it.next(); // {value: 3, done: false}
it.next(); // {value: 4, done: false}
it.next(); // {value: 5, done: false}
it.next(); // {value: undefined, done: true}
```

## 타입스크립트 (TypeScript)
- 브라우저들은 타입스크립트를 이해하지 못하기때문에 자바스크립트로 변환하여 사용하여야 한다.
> Javascript (동적언어) : 런타임에 타입 결정 / 오류 발견

```ts
 // 콜론(:) 뒤에 타입을 적는다.
function add(num1: number, num2: number) {
    console.log(num1 + num2);
}

add(1, 2);

function showItems(arr:number[]) {
    arr.forEach((item) => {
        console.log(item);
    });
}

showItems([1, 2, 3]);
```

### 기본 타입
```ts
let age: number = 30;
let isAdult: boolean = true;
let a: number[] = [1,2,3];
let a2: Array<number> = [1,2,3];

let week1: string[] = ['MON', 'TUE', 'WED'];
let week2: Array<string> = ['MON', 'TUE', 'WED'];

// 튜플 (Tuple)
let b: [string, number];

b = ['z', 1];

// void : 함수에서 아무것도 반환하지 않을때 사용함.
function sayHello(): void {
    console.log('hello');
}

// never : 항상 에러를 반환하거나, 영원히 끝나지 않는 함수의 타입으로 사용함.
function showError(): never {
    throw new Error();
}

function infLoop(): never {
    while (true) {
        // do something...
    }
}

// enum : 비슷한 값들끼리 묶어줌
enum Os {
    Window,
    Ios,
    Android
}

// null, undefined
let c: null = null;
let d: undefined = undefined;
```

### 인터페이스(Interface)
```ts
let user: object;

user = {
    name: 'xx',
    age: 30
};

console.log(user.name);
// Property 'name' does not exist on type 'object'.

// 프로퍼티를 정의해서 객체를 표현할때 interface 를 사용
// 입력을 해도/안해도 되는 옵션은 뒤에 물음표(?)를 작성
// readonly : 값에 접근을 할 수 있지만, 수정은 불가
type Score = 'A' | 'B' | 'C' | 'F'

interface User {
    name: string;
    age: number;
    gender?: string;
    readonly birthYear: number;
    [grade:number]: Score;
};

let user: User = {
    name: 'xx',
    age: 30,
    birthYear: 2000,
    1: 'A'
};

// interface 로 클래스를 정의할 수 있다.
interface Car {
    color: string;
    wheels: number;
    start(): void;
}

// extends 키워드로 Car의 속성을 받을 수 있다.
interface Benz extends Car {
    door: number;
    stop(): void;
}

// implements : 클래스의 인스턴스만 검사
class Bmw implements Car {
    color;
    wheels = 4;
    constructor(c: string) {
        this.color = c;
    }
    start() {
        console.log('go..');
    }
}

const b = new Bmw('green');
console.log(b);
// [LOG]: Bmw: {
//   "wheels": 4,
//   "color": "green"
// } 
b.start();
// [LOG]: "go.." 
```

### 함수
```ts
interface User {
    name: string;
}

const Sam: User = { name: 'Sam' };

function showName(this: User, age: number, gender: 'm'|'f') {
    // this의 타입을 정할때 함수의 첫번째 자리에 this를 쓰고 타입을 입력    
    console.log(this.name, age, gender);
}

const a = showName.bind(Sam);
a(30, 'm');

////////////////////////////////////////////////////////////
interface User {
    name: string;
    age: number;
}

// 함수 오버로드 : 전달받은 매개변수의 개수나 타입에 따라 다른 동작을 함
function join(name: string, age: number): User;
function join(name: string, age: string): string;
function join(name: string, age: number | string): User | string {
    if (typeof age === "number") {
        return {
            name,
            age
        }
    } else {
        return '나이는 숫자로 입력해주세요';   
    }
}
const sam: User = join("Sam", 30);
const jane: string = join("Jane", "30");
```

### 리터럴, 유니온/교차 타입

```ts
// Union Types

interface Car {
    name: "car";
    color: string;
    start(): void;
}

interface Mobile {
    name: "mobile";
    color: string;
    call(): void;
}

function getGift(gift: Car | Mobile) {
    console.log(gift.color);
    if (gift.name === "car") {
        gift.start();
    } else {
        gift.call();
    }
}
```
```ts
// Intersection Types

interface Car {
    name: string;
    start(): void;
}

interface Toy {
    name: string;
    color: string;
    price: number;
}

const toyCar: Toy & Car = {
    name: "타요",
    start() {},
    color: "blue",
    price: 1000
}
```

### 클래스
```ts
class Car {
    // 타입스크립트에서 멤버변수는 미리 선언해야한다.
    color: string;
    constructor(color: string) {
        this.color = color;
    }

    start() {
        console.log("start");
    }
}

const bmw = new Car("red");
```

```ts
// 접근 제한자(Access modifier) - public, private, protected
// public : 자식클래스, 클래스 인스턴스(z4)에서 접근 가능
// protected : 자식클래스 내부에서는 참조할 수 있으나 클래스 인스턴스(z4)로는 참조할 수 없음.
// private : 해당 클래스 내부에서만 사용가능
// static 을 써주면 정적멤버 변수로 만들 수 있음.
class Car {
    name: string = "car";
    color: string;
    static wheels = 4;
    constructor(color: string) {
        this.color = color;
    }
    start() {
        console.log("start");
        console.log(this.name);
        console.log(Car.wheels);   // static 이라서 Class명을 써야한다.
    }
}

// Bmw 클래스는 Car 의 속성을 받음
class Bmw extends Car {
    constructor(color: string) {
        super(color);
    }
    showName() {
        console.log(super.name);
    }
}

const z4 = new Bmw("black");
z4.name = "zzz4";
console.log(z4.name);
```

```ts
// 추상 Class
abstract class Car {
    color: string;
    constructor(color: string) {
        this.color = color;
    }
    start() {
        console.log("start");
    }
    // 이름정도만 선언하고, 구체적인 기능은 상속받은쪽에서 구현
    abstract doSomethig(): void;
}

// 추상 class는 new를 이용해서 객체를 만들 수 없다.
// 상속을 통해서만 사용가능.
// const car = new Car("red")

// Bmw 클래스는 Car 의 속성을 받음
class Bmw extends Car {
    constructor(color: string) {
        super(color);
    }
    doSomethig() {
        alert(3);
    }
}

const z4 = new Bmw("black");
```

### 제네릭 Generics
```ts
// Generic : <T> 타입 parameter를 사용한다
function getSize<T>(arr: T[]): number {
    return arr.length;
}

// 사용하는쪽에서 Generic의 타입을 결정한다.
const arr1 = [1, 2, 3];
getSize<number>(arr1);

const arr2 = ["a", "b", "c"];
getSize<string>(arr2);

const arr3 = [false, true, true];
getSize<boolean>(arr3);

const arr4 = [{}, {}, { name : "Tim" }];
getSize<object>(arr4);
```

```ts
// Generic을 사용하여 1개의 interface만 선언하고 각각 다른 객체를 만들 수 있다.
interface Mobile<T> {
    name: string;
    price: number;
    option: T;
}

const m1: Mobile<object> = {
    name: "s21",
    price: 1000,
    option: {
        color: "red",
        coupon: false
    },
};

const m2: Mobile<string> = {
    name: "s20",
    price: 900,
    option: "good"
}
```

### 유틸리티 타입 Utility Types
```ts
// keyof : interface를 Union형태로 받을 수 있다.
interface User {
    id: number;
    name: string;
    age: number;
    gender: "m" | "f";
}

type UserKey = keyof User; // 'id' | 'name' | 'age' | 'gender'

const uk: UserKey = 'name';
```

```ts
// Partial<T> : 프로퍼티를 모두 옵션으로 바꿔줌.
interface User {
    id: number;
    name: string;
    age: number;
    gender: "m" | "f";
}

let admin: Partial<User> = {
    id: 1,
    name: "Bob",    
}

// Partial<User> 는 아래와 같아진다.
// interface User {
//     id?: number;
//     name?: string;
//     age?: number;
//     gender?: "m" | "f";
// }
```

```ts
// Required<T> : 프로퍼티를 모두 필수로 바꿔줌.
interface User {
    id: number;
    name: string;
    age?: number;
}

let admin: Required<User> = {
    id: 1,
    name: "Bob",
    age: 30
}
```

```ts
// Readonly<T> : 읽기 전용으로 바꿔줌 (처음 할당만 가능, 수정을 불가능)
interface User {
    id: number;
    name: string;
    age?: number;
}

let admin: Readonly<User> = {
    id: 1,
    name: "Bob"
}
```

```ts
// Record<K,T> : K(key), T(Type)
interface User {
    id: number;
    name: string;
    age: number;
}

function isValid(user: User) {
    const result: Record<keyof User, boolean> = {
        id: user.id > 0,
        name: user.name !== '',
        age: user.age >0
    }
    return result;
}
```

```ts
// Pick<T,K> : T(Type)에서 K(key) 프로퍼티만 골라 사용
interface User {
    id: number;
    name: string;
    age: number;
    gender: "M" | "F";
}

const admin: Pick<User, "id" | "name"> = {
    id: 0,
    name: "Bob"
}
```

```ts
// Omit<T,K> : 특정 프로퍼티를 생략하고 쓸 수 있다.
interface User {
    id: number;
    name: string;
    age: number;
    gender: "M" | "F";
}

const admin: Omit<User, "age" | "gender"> = {
    id: 0,
    name: "Bob"
}
```

```ts
// Exclude<T1,T2> : T1에서 T2를 제외하고 사용하는 방식
// Omit은 프로퍼티 제거, Exclude는 타입으로 제거
type T1 = string | number | boolean;
type T2 = Exclude<T1, number | string>;
```

```ts
// NonNullable<Type> : Null을 제외한 타입을 생성

type T1 = string | null | undefined | void;
type T2 = NonNullable<T1>;
// T2는 string, void만 남게된다.
```
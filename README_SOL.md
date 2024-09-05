## 타입스크립트란?

"타입스크립트는 자바스크립트의 확장판" 자바스크립트 코드에서 타입을 정의하는 문법을 추가한 것

### JS vs TS

타입 시스템이란? 언어의 타입 관련된 문법 체계 
1. 정적 타입 시스템 : 코드 실행전에 모든 변수의 타입을 고정적으로 결정 (엄격함) ex) JAVA
2. 동적 타입 시스템 : 코드를 실행하고 나서 그때 그때마다 유동적으로 변수의 타입을 결정 (유연함) ex) JS

+ TS는 JS의 동적 타입 시스템과 JAVA의 정적 타입 시스템을 혼합한 점진적 타입 시스템 사용

### TS의 동작 과정

코드 -> AST -> 타입검사 -> 검사 성공시 AST를 JS로 변환 -> AST -> 바이트 코드 => 실행

코드에 오류가 있다면 컴파일 도중 실패하므로 js보다 안전함 (검사를 한번 더 하므로)

### 타입스크립트 설정하기
타입스크립트 컴파일러 설치하기 : sudo npm i -g typescript
>sudo란? “superuser do”의 약자, 관리자 권한(root 권한)이 필요한 명령어를 실행할 때 사용

타입스크립트 파일 실행하기 : ts-node 파일명

실습환경 설정하기 : npm init

### 원시타입 : 하나의 값만 저장할 수 있는 타입
> number, string, boolean, null, undefined

1. number 타입 : 정수, 소수, 음수 , Infinity, NaN

```ts
let num1: number = 123;
let num3: number = 0.123;
let num6: number = -Infinity;
let num7: number = NaN;
```

2. string 타입 : 문자열

```ts
let str1: string = "gd";
let str2: string = 'gd';
let str3: string = `gd`;
let str4: string = `gd ${str1}`;
```

3. boolean 타입 : true , false

```ts
let bool1 : boolean = true;
let bool2 : boolean = false;
```

4. 기타 타입 : null 타입, undefined 타입 등

```ts
let null1: null = null;
let unde1: undefined = undefined;
let numA = null;
let numA: 10 = 10;
let strA: "hello" = "hello";
let boolA: true = true;
```

### 배열과 튜플

배열 타입 정의 방법

```ts
let numArr: number[] = [1, 2, 3]
let strArr: string[] = ["hello", "ts", "world"];
let boolArr: Array<boolean> = [true, false, true];
let multiArr: (number | string)[] = [1, "hello"];
let doubleArr : number[][] = [ [1, 2, 3],  [4, 5], ];
```

튜플

```ts
let tup1: [number, number] = [1, 2];
let tup2: [number, string, boolean] = [1, "2", true];
```
+ Push, pop 메서드 사용가능
---

### 객체

객체 리터럴 타입으로 객체를 정의할 것 (구조적 타입 시스템)

```ts
let user: {
  id: number;
  name: string;
} = {
  id: 1,
  name: "likelion",
};
```

### 타입 별칭 : 변수를 선언하듯 타입을 별도로 정의 가능

```ts
let user1: User = {
  id: 1,
  name: "sol",
  nickname: "spark",
  mbti: "INTP",
};

let user2: User = {
  id: 1,
  name: "gyutae",
  nickname: "paranyo",
  mbti: "ENTJ",
};
```
>동일한 스코프에 동일한 이름의 타입 별칭 선언 안댐

### 인덱스 시그니쳐 : 객체 타입을 유연하게 정의하게 돕는 특수 문법

+ 규칙을 위반하지만 않으면 모든 객체를 허용하기 때문에 아래와 같이 빈 객체도 오류 안남
+ 필수 프로퍼티는 직접 명시
+ 인덱스 시그니처의 value타입과 직접 추가한 프로퍼티의 value타입이 호환되거나 일치해야함

```ts
type CountryCodes = {
  [key: string]: string;
};

let countryCodes: CountryCodes = {
  Korea: "ko",
  UnitedState: "us",
  UnitedKingdom: "uk",
};
```
### 열거형 타입 : 자바스크립트엔 없는 타입스크립트 한정판 , 여러개의 값을 나열하는 용도로 사용
+ 숫자 열거형 타입 : 멤버의 값이 모두 숫자인 enum
+ 문자열 열거형 타입 : enum은 컴파일시 사라지지 않고 자바스크립트 객체로 변환되므로 값으로 사용

### any와 unknown 타입
>any타입은 모든 타입스크립트의 문법과 규칙으로부터 자유롭지만, 사실상 타입 검사를 받지 않으므로 비추비추

+ unknown타입은 any와 비슷하지만 보다 안전한 타입 : 어떤 타입의 값이든 다 저장 

그러나 다른 타입의 변수에 unknown타입의 값을 저장 불가능, 연산/메서드 다 불가능

```ts
let unknownVar: unknown;

unknownVar = "";
unknownVar = 1;
unknownVar = () => {};
```
+ 타입 좁히기 : 조건문을 이용해 특정 값이 특정 타입임을 보장하기

```ts
if (typeof unknownVar === "number") {
  num = unknownVar;
}
```

### void와 never

+void : "none" 아무런 값도 반환하지 않는 함수의 반환값 타입을 정의할 때 사용

+never : "불가능" 함수가 어떠한 값도 반환할 수 없는 상황일 때 해당 함수의 반환값 타입을 정의할 때 사용

### 타입에 관하여...

+타입은 집합이다 : 타입스크립트의 모든 타입들은 집합으로써 서로 포함하고 또 포함되는 관계를 가짐

다른 타입을 포함하는 타입은 "슈퍼타입(부모타입)" , 그 반대는 "서브타입(자식타입)"

서브타입의 값을 슈퍼타입의 값으로 취급하는 것을 "업 캐스팅" , 그 반대의 경우는 "다운 캐스팅"

+타입 계층도

(계층도 이미지 넣기)

### 객체 타입의 호환성 

모든 객체 타입은 각각 다른 객체 타입들과 슈퍼-서브 타입의 관계

>업 캐스팅은 허용하고 다운 캐스팅은 허용 안댐

```ts
type Book = {
  name: string;
  price: number;
};

type ProgrammingBook = {
  name: string;
  price: number;
  skill: string;
};

let book: Book;
let programmingBook: ProgrammingBook = {
  name: "한 입 크기로 잘라먹는 타입스크립트",
  price: 33000,
  skill: "TypeScript",
};
```

+초과 프로퍼티 검사 : 타입에 정의된 프로퍼티 외의 다른 초과된 프로퍼티를 가지는 객체는 변수에 할당할 수 

### 대수 타입 : 여러개의 타입을 합성해서 만드는 타입

+ 합집합 (Union) 타입
+ 교집합(Intersection) 타입

```ts
type Dog = {
  name: string;
  color: string;
};

type Person = {
  name: string;
  language: string;
};

type Union1 = Dog | Person;

type Dog = {
  name: string;
  color: string;
};

type Person = {
  name: string;
  language: string;
};

type Intersection = Dog & Person;

let intersection: Intersection = {
  name: "",
  color: "",
  language: "",
};
```

### 타입 추론 : 타입이 정의되어 있지 않는 변수의 타입을 자동으로 추론

+변수선언 :  초기값을 기준으로 추론

+구조 분해 할당 : 객체와 배열을 구조 분해 할당하는 상황 추론

+함수의 반환값 :  return문을 기준으로 추론

+기본값이 설정된 매개변수 : 기본값을 기준으로 추론

>변수를 선언할 때 초기값을 생략하면 any타입으로 추론됨

### 타입 단언 : A as B 타입, 특정 값을 원하는 타입으로 단언

+조건 : A가 B의 슈퍼타입이다. or A가 B의 서브타입이다. 를 만족할 것

+다중 단언 : 왼쪽~오른쪽 순서 

+const 단언 : 변수를 const로 선언한 것과 비슷함

+Non Null 단언 : 값 뒤에 !를 붙여주면 이 값이 undefined이거나 null이 아닐것으로 단언 (예외)

### 서로소 유니온 타입 : (교집합이 없는 타입들) 서로소 관계에 있는 타입들을 모아 만든 유니온 타입

```ts
type Admin = {
  name: string;
  kickCount: number;
};

type Member = {
  name: string;
  point: number;
};

type Guest = {
  name: string;
  visitCount: number;
};

type User = Admin | Member | Guest;

function login(user: User) {
  if ("kickCount" in user) {
    // Admin
    console.log(`${user.name}님 현재까지 ${user.kickCount}명 추방했습니다`);
  } else if ("point" in user) {
    // Member
    console.log(`${user.name}님 현재까지 ${user.point}모았습니다`);
  } else {
    // Guest
    console.log(`${user.name}님 현재까지 ${user.visitCount}번 오셨습니다`);
  }
}
```
---

```ts
type Admin = {
  tag: "ADMIN";
  name: string;
  kickCount: number;
};

type Member = {
  tag: "MEMBER";
  name: string;
  point: number;
};

type Guest = {
  tag: "GUEST";
  name: string;
  visitCount: number;
};

function login(user: User) {
  if (user.tag === "ADMIN") {
    // Admin
    console.log(`${user.name}님 현재까지 ${user.kickCount}명 추방했습니다`);
  } else if (user.tag === "MEMBER") {
    // Member
    console.log(`${user.name}님 현재까지 ${user.point}모았습니다`);
  } else {
    // Guest
    console.log(`${user.name}님 현재까지 ${user.visitCount}번 오셨습니다`);
  }
}

switch (user.tag) {
    case "ADMIN": {
      console.log(`${user.name}님 현재까지 ${user.kickCount}명 추방했습니다`);
      break;
    }
    case "MEMBER": {
      console.log(`${user.name}님 현재까지 ${user.point}모았습니다`);
      break;
    }
    case "GUEST": {
      console.log(`${user.name}님 현재까지 ${user.visitCount}번 오셨습니다`);
      break;
    }
  }

```






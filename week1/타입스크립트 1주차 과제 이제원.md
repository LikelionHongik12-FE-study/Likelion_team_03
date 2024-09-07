# Likelion_team_03

https://www.notion.so/type-script-e3a8da28cc604df1becb23a62cc9da89?pvs=4

### 컴파일러 옵션 설정

- tsc - -init → tsconfig.json 파일 생성  → tsconfig.json 파일 새로 구성하기
- tsconfig 파일 설정

```
{
  "compilerOptions":{    
    "target":"ESNext",   //컴파일러 버전 설정
    "module":"ESNext",   //import,export 할떄 어떤 문법을 사용할 것인지
    "outDir":"dist",   //compile한 결과물인 js파일들을 dist라는 폴더에 따로 보관
    "strict": true,    //타입에 대한 엄격한 검사여부
    "moduleDetection": "force"  //ts파일들을 독립된 파일들로 보기위한 조치
  },
  "include": ["section1/src"]   //컴파일 경로 설정
}
```

- section3
    
    ### 기본타입
    
    - 원시타입
        - number /  string / boolean / null / undefined
        - "strictNullChecks": false  //null 타입이 아닌 변수에 null값 허용 가능
        
        ```tsx
        {
          "compilerOptions":{    
            "target":"ESNext",   //컴파일러 버전 설정
            "module":"ESNext",   //import,export 할떄 어떤 문법을 사용할 것인지
            "outDir":"dist",   //compile한 결과물인 js파일들을 dist라는 폴더에 따로 보관
            "strict": true,    //타입에 대한 엄격한 검사여부
            "moduleDetection": "force",  //ts파일들을 독립된 파일들로 보기위한 조치
            "strictNullChecks": false  //null 타입이 아닌 변수에 null값 허용 여부
          },
          "include": ["section2/src"]   //컴파일 경로 설정
        }
        ```
        
        <aside>
        💡 literal 타입 → let numA: 10 =10; //numA에는 10 이외의 값은 넣을 수 없음
        
        </aside>
        
    - 배열과 튜플
        - 튜플은 배열의 타입을 명시적으로 표시해줄때 유용
        
        ```
        //배열
        let numArr: number[]=[1,2,3];
        
        let boolArr: Array<boolean> =[true,false,true];
        
        //배열에 들어가는 요소들의 타입이 다양할 경우
        let multiArr: (number | string)[]=[1,"hello"];
        
        //다차원 배열의 타입을 정의하는 방법
        let doubleArr: number[][]=[
            [1,2,3],
            [4,5],
        ];
        
        //튜플 -> 길이와 타입이 고정된 배열
        let tup1:[number,number]=[1,2];
        let tup2:[number,string,boolean]=[1,"hello",true];
        
        ```
        
    
    - 객체
        - 
        
        ```
        //object -> 객체를 정의할때 이건 잘 사용하지 않음
        //객체 리터럴 타입 -> 구조를 기준으로 객체 정의(구조적 타입 시스템)
        let user:{
            id?:number;  //선택적 option을 위해 ?를 추가
            name:string
        }={
            id:1,
            name:"이제원",
        };
        
        let dog:{
            name:string;
            color:string
        }={
            name:"돌돌이",
            color:"brown",
        }
        
        user={ //현재 여기에는 id를 정의하지 않음 -> 이를 해결하기 위해 user구조에서 id에 ?를 추가
            name:"고길동"
        }
        
        let config: {
            readonly apiKey: string;
        }={
            apiKey: "My apiKey",
        };
        
        config.apiKey="hacked"; //readonly이므로 이렇게 다른 값으로 수정 불가
        
        console.log(user.id);
        console.log(dog.color);
        
        ```
        
    
    - 타입 별칭과 인덱스 시그니처
        - 
        
        ```
        //타입 별칭
        type User={
            id: number;
            name:string;
            nickname:string;
            birth:string;
        };
        
        let user:User={
            id:2,
            name:"이제원",
            nickname:"고돌",
            birth:"2000",
        };
        
        //인덱스 시그니처
        type CountryCodes={   
            [key:string]:string;
        };
        
        let countryCodes: CountryCodes={
            korea:"ko",
            UnitedStates:"us",
        };
        ```
        
    - Enum(열거형) 타입
        - 
        
        ```
        enum Role{
            ADMIN=0,
            USER=1,
            GUEST=2,
        };
        
        const user1={
            name: "이제원",
            role: Role.ADMIN,
        };
        
        const user2={
            name:"홍길동",
            role: Role.USER,
        };
        
        const user3={
            name:"아무개",
            role:Role.GUEST,
        };
        
        console.log(user1,user2,user3);
        ```
        
    - Any/Unknown
        - 
        
        ```
        //any
        //특정 변수의 타입을 우리가 확실히 모를떄
        //최대한 사용은 지양
        
        let anyVar: any=10;
        anyVar="hello";
        
        //unknown
        //unKnownVar.toUpperCase() 이런것들 사용 불가 -> 조금 더 안전하게 사용하고 싶으면
        //any 대신 unknown 타입 사용
        let unknownVar: unknown;
        ```
        
    - void/Never
        - 
        
        ```
        //void
        function func1(): string{
            return "hello";
        }
        
        function func2(): void{  //return값이 없을때 사용 가능
            console.log("hello");
        }
        
        //never
        //불가능한 타입(존재하지 않는)
        
        function func3(): never{
            while(true){}
        }
        
        function func4(): never{
            throw new Error();
        }
        ```
        
- section4
    
    ### 타입은 집합이다
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/171f996f-c2e1-4622-8f58-6654c9fc94c5/308de52a-2b5a-44ee-b13e-bdb9f267bc53/image.png)
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/171f996f-c2e1-4622-8f58-6654c9fc94c5/e884571c-57e8-4296-a4c8-387f1bede34d/image.png)
    
    - 계층도를 이해하기 위한 코드
    
    ```tsx
    
    //unknown 타입
    
    function unknownExam(){
        let a: unknown=1;
        let b: unknown="hello";
    }
    
    //never 타입
    
    function neverExam(){
        function neverFun(): never{
            while(true){}
        }
    }
    
    //void 타입
    
    function voidExam(){
        function voidFunc():void{
            
        }
    
        let voidVar: void = undefined;
    }
    
    //any 타입
    
    function anyExam(){
        let unknownVar: unknown;
        let anyVar: any;
        let undefinedVar: undefined;
        let neverVar: never;
    
        anyVar=unknownVar;  //any타입은 다운캐스팅이 가능하다 -> 타입 계층도를 완전히 무시한다
        undefinedVar=anyVar;
    
        //neverVar =anyVar; 하지만 never타입은 다운캐스팅이 불가능하다(아무리 any타입이 함께여도)
        
    }
    
    ```
    
    ### 객체 타입의 호환성
    
    ```tsx
    //객체 타입간의 호환성
    
    type Animal={
        name: string;
        color: string;
    };
    
    type Dog={
        name:string;
        color:string;
        breed:string;
    };
    
    let animal: Animal={
        name: "기린",
        color: "yellow",
    };
    
    let dog: Dog={
        name:'돌돌이',
        color:'red',
        breed:'진도',
    };
    
    animal=dog;
    
    //dog=animal; //이렇게는 불가능-> Animal객체가 Dog객체보다 부모(property가 더 적으면 부모...)  
    
    //초과 property검사
    //위와 같이 animal=dog는 가능
    //하지만 아래와 같은 경우 초과 프로퍼티 검사로 인해 오류 발생
    /* let dog2: Animal={
        name:'아아',
        color:'blue',
        breed:'허스키',
     }*/
    
    ```
    
    ### 대수 타입
    
    ```tsx
    //1.합집합 -> union타입
    
    let a: string | number;
    a=1;
    a="하나";
    
    type Dog = {
        name:string;
        color:string;
    };
    
    type Person={
        name:string;
        language:string;
    };
    
    type Union1= Dog | Person
    
    let union1: Union1={
        name:'',
        color:'',
    };
    
    let union2: Union1={
        name:'',
        language:'',
    };
    
    let union3: Union1={
        name:'',
        color:'',
        language:'',
    };
    
    /* let union4: Union1={    //이것은 Union1집합 어느곳에서도 포함되지 않는 객체이므로 오류
         name:'',
     }*/                            
    
    //2.교집합 -> intersection 타입
    
    let variable: number & string;  //이때는 number타입과 string타입이 공유하는게 없으므로 never 타입
    
    type Intersection=Dog & Person;
    
    let intersection1: Intersection={
        name:'',
        color:'',
        language:'',  //여기서 language를 빼면 오류 -> language를 빼버리면 Person에 해당하지 않게 되기 떄문
    }
    
    ```
    
    ### 타입 추론
    
    - 초기 할당값으로 타입을 추론
    - 초기 할당값이 없을시에는…
        - any의 진화
        
        ```tsx
        let d;
        // 암시적인 any 타입으로 추론
        d = 10;  //이때는 number타입
        d.toFixed();  
        
        d = "hello";  //이때는 string 타입
        d.toUpperCase();
        //d.toFixed(); // 오류 
        ```
        
    
    ### 타입 단언
    
    ```tsx
    type Person = {
      name: string;
      age: number;
    };
    
    let person = {} as Person;
    person.name = "";
    person.age = 23;
    ```
    
    - 오류발생 코드
    
    ```tsx
    type Dog = {
      name: string;
      color: string;
    };
    
    let dog: Dog = {  
    	name: "돌돌이",
      color: "brown",
      breed: "진도",
    }    // 여기서 초과 프로퍼티 검사로 인해 오류발생
    ```
    
    - 타입 단언을 통한 오류 해결
    
    ```tsx
    type Dog = {
      name: string;
      color: string;
    };
    
    let dog: Dog = {
      name: "돌돌이",
      color: "brown",
      breed: "진도",
    } as Dog   // as로 타입 단언을 해주면 오류 없앨 수 있음
    	
    	/*let dog = {
      name: "돌돌이",
      color: "brown",
      breed: "진도",
    	} as Dog
    */  //이렇게도 가능
    ```
    
    - 타입 단언의 규칙
        - 값 as 단언  → A as B
        - A가 B의 슈퍼타입이거나
        - A가 B의 서브타입이어야 함
    
    - 다중단언 → 별로 좋지 않은 방법
        
        `let num3 = 10 as unknown as string;`
        
    
    - const 단언
        
        ```tsx
        let cat = {
          name: "야옹이",
          color: "yellow",
        } as const;
        // 모든 프로퍼티가 readonly를 갖도록 단언됨
        ```
        
    
    - **Non Null 단언**
        
        ```tsx
        type Post = {
          title: string;
          author?: string;
        };
        
        let post: Post = {
          title: "게시글1",
        };
        
        const len: number = post.author!.length;
        //!를 통해 author 프로퍼티가 있다고 강조
        ```
        
    
    ### 타입 좁히기
    
    - Date 객체는 instanceof를 사용해야 함
        - value에 null값도 올 수 있으므로
    - 직접 정의한 Person 객체의 경우 in을 사용해야함
        - age라는 프로퍼티를 가지는 value는 Person타입 밖에 없기 때문
        - 추가로 value는 null이 아님을 표시하기 위해 조건문에 value 부분 추가
    
    ```tsx
    type Person = {
      name: string;
      age: number;
    };
    
    function func(value: number | string | Date | null | Person) {
      if (typeof value === "number") {
        console.log(value.toFixed());
      } else if (typeof value === "string") {
        console.log(value.toUpperCase());
       } else if (value instanceof Date) {
        console.log(value.getTime());
    	 } else if (value && "age" in value) {
        console.log(`${value.name}은 ${value.age}살 입니다`)
      }
    }
    ```
    
    ### 서로소 유니온 타입
    
    - ex) string ↔ number 타입
    - tag 프로퍼티를 통해 세종류의 타입들이 교집합 없이 각각의 집합으로 구분되게 함
    
    ```tsx
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
    
    type User=Admin | Member | Guest
    ```
    
    ```tsx
    function login(user: User) {
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
    }
    ```

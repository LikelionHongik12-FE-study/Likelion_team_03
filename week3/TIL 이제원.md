# tailwind CSS

## tailwind CSS란?

- **Utility-First 컨셉을 가진 CSS 프레임워크**
- 미리 세팅된 유틸리티 클래스를 활용하는 방식으로 HTML 코드 내에서 스타일링이 가능

## 유틸리티 클래스 기반 프레임워크?

- CSS의 각 스타일 속성을 독립적인 "유틸리티 클래스"로 제공하는 방식을 사용하는 프레임워크

## 장점

- **간단한 스타일 적용**
    - 기존 css를 사용할때는 태그들의 클래스명을 하나하나 지정해주어야 하는 번거러움이 존재
    - 미리 세팅된 유틸리티 클래스를 활용하는 방식으로 스타일링이 간편하다
    - tailwind CSS를 사용하면 아래와 같이 클래스 네임을 지정해주지 않고도 바로 인라인 스타일로 스타일을 지정할 수 있다.
    
    ```html
    <body>
         <div class="bg-gradient-to-r from-yellow-400 to-red-400"></div>
    </body>
    ```
    
- **파일을 별도로 관리할 필요가 없다**
    - HTML 파일과 CSS파일을 왔다갔다 하며 코딩을 하지 않아도 된다.
- **위와 같은 장점들로 인해 프로그래밍 속도가 월등히 높아지는 효과를 얻을 수 있음**

## 단점

- **가독성**
    - className 자리 대신 그곳에 인라인 스타일링을 해주다 보니 코드의 가독성이 나빠진다.
- **유지보수의 어려움**
- **스타일 재사용의 어려움**
    - 이전 css 방식에서는 예를 들어 같은 모양의 버튼을 만드는 경우 button class에 대한 스타일링을 한번만 해주고 그것을 재사용하는 방식
    - 하지만 tailwind CSS를 사용하면 모든 버튼에 스타일링을 해줘야 하며 스타일에 변경 사항이 있을시 모든 버튼을 수정해줘야 하는 번거러움   → **단**, **이 문제는 html 반복문과 같은 방식을 통해 해결가능**
- **익히는데 시간이 조금 필요함**

## 사용방법

```html
<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
		버튼입니다!
</button>
```

- `bg-blue-500`: 배경색을 파란색(500)으로 설정
- `hover:bg-blue-700`: 호버할 때 배경색을 파란색(700)으로 변경
- `text-white`: 글자 색을 흰색으로 설정
- `font-bold`: 폰트를 굵게 설정
- `py-2`: 상하 패딩을 2 단위로 설정 (1단위 → 4px 기준)
- `px-4`: 좌우 패딩을 4 단위로 설정
- `rounded`: 모서리를 둥글게 설정

https://tailwindcss.com/docs/installation  → 추가 스타일 사용 방식은 공식문서에서 찾아 볼 수 있음

## 스타일 커스터마이징

- **tailwind.config.js 파일 생성**
- 원하는 스타일링 커스터마이징
    - 기존 스타일에 추가로 값을 넣어줄 경우에는 extend 객체 안에 넣어줘야 한다.

```jsx
module.exports = {
theme: {
extend: {
spacing: {
'3px': '3px',
'7px': '7px',
},
},
},
}
```

이렇게 하면  `p-3px`, `m-7px` 등으로 3px 또는 7px 간격을 적용할 수 있다.

```jsx
module.exports = {
theme: {
extend: {
colors: {
customGreen: '#32a852',
customBlue: '#0044cc',
},
},
},
}
```

색상도 추가 가능

## JIT 모드

**Just-In-Time**

- JIT 모드를 사용하지 않았을시
    - 아래와 같이 `config.js`파일에 색상을 커스터마이징을 해준 후 사용

```jsx
module.exports = {
purge: [],
theme: {
extend: {
colors: {
customBlue: PALETTE.skyblue
}
}
}
}
```

```html
function App() {
  return (
  <figure className="md:flex bg-customBlue rounded-xl p-8 md:p-0">
      ...
    </figure>
  );
}

export default App;
```

- JIT 모드 사용했을 시
    - 별도의 속성 추가 없이 커스터마이즈 가능
    - JIT 모드 설정을 위해서는 **`tailwind.config.js`** 에 mode: "jit" 이라는 속성을 직접 정의한 후, purge 설정에는 테일윈드를 적용할 모든 경로 및 파일을 지정해줘야
    
    ```jsx
    module.exports = {
    purge: [
    './public/**/*.html',
    './src/**/*.{js,jsx,ts,tsx,vue}',
    ],
    mode: "jit"
    }
    ```
    
    ```html
    function App() {
      return (
    	// 속성명-[커스텀할 값] 으로 테일윈드 클래스명을 직접 커스텀
        <figure className="md:flex bg-[#bae4f5] rounded-xl p-8 md:p-0">
          ...
        </figure>
      );
    }
    
    export default App;
    ```
    
    <aside>
    💡
    
    **JIT 모드를 사용 가능한 조건)**
    
    테일윈드 CSS는 런타임 중 클라이언트의 어떤 영향(변수, 조건문 등)도 받지 않으므로, 빌드 타임에서 추론이 가능한 클래스명을 정적으로 지정해야 한다
    
    </aside>
    
    ### Tailwind CSS의 기본 동작 방식
    
    - Tailwind의 스타일은 사전 정의된 클래스를 통해 적용되며, 이러한 클래스는 빌드 타임에 CSS 파일로 컴파일
    
    ```html
    function App() {
    return (
    <figure className={md:flex bg-${[PALETTE.skyblue]} rounded-xl p-8 md:p-0}>
    ...
    </figure>
    )
    }
    ```
    
    - 위 예시에서 tailwind JIT는 `PALETTE.skyblue`의 실제 값을 컴파일 타임에 알지 못한다. → `PALETTE.skyblue` 는 클래스 이름을 동적으로 생성하려고 하기 때문

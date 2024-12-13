###### Fragment
- 컴포넌트 내의 return문에 존재하는 div태그는 제거해도 괜찮지 않을까?
	- 지우는 순간 에러가 발생한다.
		- 결국 함수인데, 두 개 이상의 형제요소를 반환하려고 하면 당연히 오류 발생
		- 대신, div태그가 중복되어 나타난다
			- Fragment를 사용하면 묶는 기능 + div 태그 중복 X의 기능을한다.
- 사용법
```jsx
return(<div>...content</div>);
return(<Fragment>...content</Fragment>);
return(<>...content</>);
```

- 컴포넌트는 상향식으로 개발하는게 좋은 듯
	- 작은 컴포넌트 > 중간 컴포넌트 > 큰 컴포넌트 로 묶어서 사용.
	- 이렇게 되면 App.js는 매우 깔끔한 상태가 된다.
- 반복되는 형식은 모두 컴포넌트로 생성
	- 컴포넌트의 대부분이 section - h2 - menu 형식으로 구현되어 있음
- CSS 설정 때문에 id를 props로 넘긴다? :: 매우 비효율 => Forwarded Prorps(Proxy Props 패턴) 사용으로 대체
- 스프레드 연산자 + 변수명을 props를 받은 후 태그에 사용하면, CSS가 적용됨
- JSX는 Props로 JSX를 넘겨줄 수 있는데, 이것 또한 하나의 요소만 들어갈 수 있다.

- 컴포넌트 타입을 const로 생성할 수 있다. (소문자로 시작)
	1. 상위에서 ""로 요소를 props로 전달
	2. 하위에서는 해당 props를 상수로 만들든, 구조분해로 값을 할당하든 해서 새로운 Wrapper 변수 생성
	3. 해당 이름 및 변수로 Wrapper 사용 가능
```JSX
/* 상위 컴포넌트 */
<Test testpp="div"></Test>
/* 하위 컴포넌트 */
const Cpnm = ({ testpp, testppp=testpp }) => {
const testppp = testpp;
return(
	<>
		<testpp></testpp>
		<testppp></testppp>
	</>
	)
}
```

**정적 파일 위치**
- public/ : 개발 서버 및 빌드 프로세스에 의해 공개적으로 제공
- src/ : src 하위 폴더는 비공개, 빌드 프로세스에 의해 최적화 되어 웹사이트에 제공하기 직전에 public에 삽입 -> 링크 생성
>**빌드 프로세스에 의해 처리되지 않는** 이미지는`public/`폴더를 사용해야 하고 **대체적으로 사용 가능** 가능합니다. 예를 들면 `index.html` 파일이나 파비콘과 같은 이미지가 좋은 후보
 반면, **컴포넌트 내**에서 사용되는 이미지는 일반적으로`src/`폴더(예: `src/assets/`)에 저장

==**동일한 마크업 또는 형식이 반복되는 경우, 새로 컴포넌트를 생성하는 것이 좋다.**==

- 컴포넌트를 한 번 혹은 여러 번 사용할 때마다, 리액트는 새로운 instance(인스턴스)를 생성합니다
	- 같은 컴포넌트를 사용하더라도, 고유하게(따로) 작동함
- 상태 처리에 대한 React 최적의 방식
	- setSomething(!something) : X
		- JSX 로드 시 실행되어 자동적으로 상태 값을 갖게 됨
	- setSomething(() => !something) : O
		- 매개변수로 인식되어 자동적으로 상태 값을 가지지 않음


***!! set메서드 인자로 함수를 래핑해서 넣어야하는 이유***
> 상태 업데이트의 **작동 방식**과 **React 상태 관리의 비동기 특성**

**1. React 상태 업데이트의 특성**
React에서 `setState` 함수는 **비동기적**으로 작동합니다. 이는 다음 두 가지 의미를 가집니다:
- `setState` 호출 시, React는 즉시 상태를 업데이트하지 않고 **스케줄**합니다.
- 현재 상태를 바로 업데이트하지 않으므로, 컴포넌트 내 `something` 변수가 업데이트 후 최신 상태를 보장하지 않습니다.
---
**2. `setSomething(!something)`의 동작**
이 방식은 상태를 직접 참조해서 반전시키는 코드입니다. 예를 들어, `something`이 `true`라면 `!something`은 `false`로 평가됩니다.
**문제점: 오래된 상태 참조**
React의 비동기 상태 업데이트 특성 때문에, 연속된 상태 업데이트가 발생하면 **이전 상태(`something`)가 정확하지 않을 수 있습니다.**
```JSX
setSomething(!something); // something의 값이 정확하지 않을 가능성이 있음
```
**연속 호출 시 문제**
상태 업데이트가 즉시 반영되지 않으므로, 같은 `something` 값을 참조하는 모든 `setSomething` 호출은 **동일한 값을 기반으로 동작**합니다.
```JSX
const [count, setCount] = useState(0);  
const incrementTwice = () => {   
	setCount(count + 1);   
	setCount(count + 1); // 이전 상태(count = 0)에 기반 
	};
```
- 위 코드는 두 번 `setCount`를 호출했지만, `count` 값은 `1`로 업데이트됩니다. `setCount(count + 1)`이 호출될 때 `count`가 여전히 `0`이기 때문입니다.
---
**3. `setSomething((prev) => !prev)`의 동작**
이 방식은 **함수형 업데이트**를 사용합니다. `setSomething` 함수에 콜백을 전달하면, React는 이 콜백에 **최신 상태 값(`prev`)**을 전달합니다.
**장점: 최신 상태 보장**
React는 상태 업데이트의 순서를 보장하므로, 각 콜백에서 항상 최신 상태를 참조합니다.
```
setSomething((prev) => !prev); // React가 prev에 최신 상태를 전달
```
**연속 호출 시 동작**
함수형 업데이트를 사용하면, 각 `setSomething` 호출이 서로 독립적이며 최신 상태를 정확히 반영합니다.
```JSX
const [count, setCount] = useState(0);  
const incrementTwice = () => {   
	setCount((prev) => prev + 1);   
	setCount((prev) => prev + 1); // 이전 콜백의 결과를 기반으로 동작 
};
```
- 여기서는 `setCount((prev) => prev + 1)` 두 번 호출되며 `count`는 `2`로 업데이트됩니다.
---
**4. 두 방식 비교 요약**

| 속성               | `setSomething(!something)` | `setSomething((prev) => !prev)` |
| ---------------- | -------------------------- | ------------------------------- |
| **상태 참조 방식**     | 현재 상태(`something`)를 사용     | 이전 상태(`prev`)를 사용               |
| **비동기적 상태 업데이트** | 현재 상태 값이 오래될 가능성 있음        | 항상 최신 상태(`prev`) 참조 가능          |
| **연속 호출 시 동작**   | 같은 상태 값 기반으로 동작            | 각 호출이 독립적으로 처리됨                 |
| **React 권장 여부**  | 권장하지 않음                    | 권장됨                             |

---
**5. 실제 예제 시나리오**
문제 상황: 상태 충돌


`const [isToggled, setIsToggled] = useState(false);  const toggleTwice = () => {   setIsToggled(!isToggled); // 첫 번째 호출: isToggled = true   setIsToggled(!isToggled); // 두 번째 호출: 여전히 isToggled = true를 참조 };`

- `toggleTwice` 실행 후 `isToggled`는 `false`가 아니라 여전히 `true`입니다. 이는 두 번의 호출이 모두 같은 `isToggled` 값을 참조했기 때문입니다.

---

### 해결책: 함수형 업데이트
```JSX
const toggleTwice = () => {
  setIsToggled((prev) => !prev); // 첫 번째 호출: prev = false → true
  setIsToggled((prev) => !prev); // 두 번째 호출: prev = true → false
};
```
- `toggleTwice` 실행 후 `isToggled`는 예상대로 `false`가 됩니다. `prev`는 항상 최신 상태를 참조하기 때문입니다.
---
**결론**
React 상태를 업데이트할 때:
1. 상태 업데이트가 이전 상태에 의존하는 경우, **반드시 함수형 업데이트**를 사용하세요.
2. `setSomething(!something)`은 직관적이지만, 상태 충돌 문제를 유발할 수 있습니다.
3. React 권장 방식인 `setSomething((prev) => !prev)`를 사용하면 안정적이고 예측 가능한 상태 업데이트가 가능합니다.

`양방향 렌더링`
onsole.log(event.target.value); : HTML 요소 JS에서 추출

아 그러면 setGameBoard는 내부적으로 const setGameBoard = (콜백함수) => { 1. 큐에 등록 2. 콜백함수 3. 리턴 값 적용 } 이런 식으로 구현되어있는 거구나


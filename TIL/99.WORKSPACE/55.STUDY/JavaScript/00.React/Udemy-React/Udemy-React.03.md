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
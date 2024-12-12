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
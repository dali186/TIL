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


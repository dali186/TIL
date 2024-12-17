**디버깅**
- Strict Mode(엄격 모드)
- ReactDevTools
- 개발자 도구
	- 흐름진행 : `F10`, `Ctrl + '`
	- 함수진입 : `F11`, `Ctrl + ;`
	- 함수탈출 : `Shift + F11`, `Ctrl + Shift + ;`
###### 리액트 컨텍스트
**Prop Drilling?**
- 하위 자식 컴포넌트에게 데이터를 전달하기 위해서 중간에 존재하는 컴포넌트가 속성을 전달해주는 것(중간 컴포넌트는 해당 데이터가 필요하지 않음.)
	- 재사용이 힘들어진다.
	- 보일러 플레이트가 늘어난다.
**Prop Drilling 해결 방안**
1. Components의 합성 (Component Composition)
	- 상위 컴포넌트, 하위 컴포넌트, 최하위 컴포넌트가 존재할 때,
		- 하위 컴포넌트 내부에 존재하는 최하위 컴포넌트를 상위 컴포넌트에서 하위 컴포넌트 태그 사이에 해당 로직을 추가
		- 필요한 함수, 변수들은 최하위 컴포넌트에서 상위 컴포넌트로 이동
		- 하위 컴포넌트에서는 children props로 태그 안에 추가해주어야 함.
		```JSX
		//TO-BE
		<Middle doSomething={handleDoSomething}/>
		//AS-IS, 함수,변수 이동
		<Middle>
			<Bottom doSomething={handleDoSomething}/>
		</Middle>
		```
2. React Context API
	- Context는 최상위에 존재하여, state를 Context에 연결하기만 하면 App 전체에 제공해줌
		- .Provider
			- 기본값을 설정했더라도, value={{}} 속성을 추가해주어야 함
	- 컴포넌트에 직접 prop으로 전달해주는것이 아니라, <Context객체.Provider>로 감싸서 제공해준다.
	- App 전체를 컴포넌트로 감싸는 건 너무 무거운 컴포넌트가 됨
		- 모든 상태와 컨텍스트 값의 관리코드를 따로 분리하여 관리(childern 속성 이용) => return <Context.Provider>
3. useReducer()
	- `reducer`: 복잡한 값을 더 단순한 형태로 만드는 함수
	- const [상태, distpatch함수] = useReducer(커스텀리듀서함수(state, action));
		- 상태 업데이트를 위해 함수 형태를 사용하여 최신으로 보장된 상태 스냅샷이 생길 때 리듀서
###### 리덕스(Redux)란?
> A state management system for cross-component or app-wide state
> 크로스 컴포넌트 또는 앱 와이드 상태를 위한 상태 관리 시스템

- Local State
	- 하나의 컴포넌트에 속하는 UI에 영향을 미치는 상태
		- 예시: 토글
- Cross-Component State
	- 다수의 컴포넌트 UI에 영향을 미치는 상태 
		- 예시: 모달(트리거의 위치가 상/하위, prop chain)
- App-Wide State
	- 모든 컴포넌트에 영향을 미치는 상태
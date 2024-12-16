**디버깅**
- Strict Mode(엄격 모드)
- ReactDevTools
- 개발자 도구
	- 흐름진행 : `F10`, `Ctrl + '`
	- 함수진입 : `F11`, `Ctrl + ;`
	- 함수탈출 : `Shift + F11`, `Ctrl + Shift + ;`
###### 리액트 컨텍스트
**Prop Drilling?**


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
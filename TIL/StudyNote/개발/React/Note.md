###### 프로젝트 구조
- `node_modules` : 라이브러리
- `public`: 정적파일(컴파일 필요 X)
- `src` : JS로 컴파일되는 파일들
	- `components`: 재사용 가능한 컴포넌트가 위치
	- `assets`: 이미지, 폰트 등 컴포넌트 내부에서 사용하는 파일
	- `hooks(=hoc)`: 커스텀 hook이 위치
	- `pages`: react router 등을 이용하여 라우팅을 적용할 때 페이지 컴포넌트들이 위치
	- `constatns` : 공통 상수 위치
	- `config` : 설정 파일
	- `styles` : css
	- `services(=api)` : API 관련 로직의 모듈 위치
	- `utils` : 공통 유틸 파일 위치
	- `contexts` : 상태관리
	- `App.js`
	- `index.js`
- `package.json`: 프로젝트 기본 내용 + 라이브러리 목록

### 클래스형 컴포넌트
---
1. `props`, `state`
	Component의 상태 정보를 가지고 있는 *멤버 변수*, 변경 시 render 함수가 다시 호출(**하위 Component까지 모두**)
	**`props`**
	- 상위 Component가 하위 Component에게 전달하면 생성되는 변수, ==하위 Component에서는 `props` 값을 수정할 수 없음.==
		```
		#상위 컴포넌트
		<Title title="Title Prop" />
		#하위 컴포넌트
		...
		{this.props.title}
		```
	**`state`**
	- 해당 Component가 직접 생성해서 사용하는 변수, ==수정이 가능.==
		```
		#생성 시,
		class Component01 extends Component {
			constructor(props) {
				super(props);
				
				#state 변수 초기화
				this.state = {
					state01: "state01" ,
					state02: "state01" ,
					};
				}
			}
		```
		
		```
		#사용 시,
		...
		{this.state.state01}

		# 수정 시,
		onClick={()=>{this.setState({state01})}}
		```
2. `event`
	하위 Component에서 상위 Component로 전달(props 넘겨주듯이)
	**`event`**
	- 상위 Component에서는 이벤트가 발생한 뒤 동작할 함수를 정의해주면 된다.
	```
	# 상위 Component
	<ChildComponent afterEvent={(res)=>{this.setAppText(res)}}
	# 하위 Component
	onClick={()=>{this.props.afterEvent('결과전송');}}
	```

##### 차트 그리기
0. 라이브러리, Import
```
npm install apexcharts
npm install react-apexcharts

import ApexCharts from 'react-apexcharts'
```

### 함수형 컴포넌트
---
![[react-lifecycle.png]]
#### useEffect()
**1. 첫 렌더링일 때만 호출 (componentDidMount)**
- 2번째 인자에 빈 배열을 추가
```
    useEffect(() => {
        alert('처음 호출됨');
    }, []);
```
**2. 모든 렌더링일 때 호출 (componentDidMount, componentDidUpdate, componentWillUnmount)**
- 2번째 인자를 생략
```
# 2번째 인자를 생략하면 재 렌더링 즉, 이벤트가 발생하는 모든 때에 호출된다
    useEffect(() => {
        alert('재렌더링');
    });
```
**3. 특정 값이 바뀔 때만 호출**


# 2번째 인자를 특정 값으로 설정하면 특정 값(props, state)가 바뀔 때만 호출된다.
    useEffect(() => {
        alert('재렌더링');
    }, [test]);
# 2번째 인자를 특정 값으로 설정하면 특정 값(props, state)가 바뀔 때만 호출된다.
    useEffect(() => {
        alert('재렌더링');
    }, [test]);
```

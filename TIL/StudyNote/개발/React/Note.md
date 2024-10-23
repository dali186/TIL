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
		```
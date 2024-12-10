**React의 컴포넌트와 파일 구조**
	1. HTML + Vanilla JS => HTML 파일, JS 파일을 번갈아가면서 수정해야 함
	2. React JS => 파일 하나만 수정하여 반영 가능
- **`index.html`**: 제목, 아이콘, `script` 태그 등 기본 구성.
- **`index.jsx`**: React의 최상위 컴포넌트(App.jsx)를 `root`에 렌더링.
- **`App.jsx`**: 화면에 보이는 실제 JSX 요소 작성.

**React 실행 과정**
> 1. JSX 코드 작성 
> 2. 빌드 
> 3. JavaScript로 변환(컴파일) 
> 4. 클라이언트(브라우저)에게 응답

**컴포넌트 동작 과정**
> 1. index.html 로드(<script type="module" src="index.jsx"></script>)
> 2. index.jsx 로드: root요소에 <App /> 컴포넌트를 렌더링
> 3. App.jsx 로드: 화면에 보여주는 요소 로드
- 최상위 컴포넌트 App 아래에 자식 컴포넌트들이 붙어있음
- 컴포넌트 트리는 리액트가 분석, 개발자 도구로 확인했을 때 커스텀 컴포넌트 요소를 확인할 수 없음(대문자로 시작하는 태그 발견 불가)
- <head></head>, <image />, <div></div>등과 같은 내장 컴포넌트는 리액트에서 DOM 노드로서 렌더링 된다
- 커스텀 컴포넌트는 단순한 함수로, 리액트에서 함수로서 실행 됨


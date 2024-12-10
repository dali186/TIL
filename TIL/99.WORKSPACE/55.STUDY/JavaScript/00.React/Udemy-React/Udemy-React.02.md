컴포넌트
	HTML + Vanilla JS => HTML 파일, JS 파일을 번갈아가면서 수정해야 함
	React JS => 파일 하나만 수정하여 반영 가능

`index.html`: 제목, 아이콘, script 태그 제외하고는 별게 없음
`index.jsx`: App.jsx를 import 하며, root에 렌더링하는 코드 존재
`App.jsx`: 실제로 화면에 보이는 html 요소가 존재

> 1. JSX 코드 작성 
> 2. 빌드 
> 3. JavaScript로 변환(컴파일) 
> 4. 클라이언트(브라우저)에게 응답

> 1. index.html 로드(<script type="module" src="index.jsx"></script>)
> 2. index.jsx 로드: root요소에 <App /> 컴포넌트를 렌더링
> 3. App.jsx 로드: 화면에 보여주는 요소 로드
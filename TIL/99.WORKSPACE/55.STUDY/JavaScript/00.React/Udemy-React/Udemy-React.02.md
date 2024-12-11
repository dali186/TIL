###### React의 컴포넌트와 파일 구조
	1. HTML + Vanilla JS => HTML 파일, JS 파일을 번갈아가면서 수정해야 함
	2. React JS => 파일 하나만 수정하여 반영 가능
- **`index.html`**: 제목, 아이콘, `script` 태그 등 기본 구성.
- **`index.jsx`**: React의 최상위 컴포넌트(App.jsx)를 `root`에 렌더링.
- **`App.jsx`**: 화면에 보이는 실제 JSX 요소 작성.
###### React 실행 과정
> 1. JSX 코드 작성 
> 2. 빌드 
> 3. JavaScript로 변환(컴파일) 
> 4. 클라이언트(브라우저)에게 응답
###### 컴포넌트 동작 과정
> 1. index.html 로드(<script type="module" src="index.jsx"></script>)
> 2. index.jsx 로드: root요소에 <App /> 컴포넌트를 렌더링
> 3. App.jsx 로드: 화면에 보여주는 요소 로드
- 최상위 컴포넌트 App 아래에 자식 컴포넌트들이 붙어있음
- 컴포넌트 트리는 리액트가 분석, 개발자 도구로 확인했을 때 커스텀 컴포넌트 요소를 확인할 수 없음(대문자로 시작하는 태그 발견 불가)
- <head></head>, <image />, <div></div>등과 같은 내장 컴포넌트는 리액트에서 DOM 노드로서 렌더링 된다
- 커스텀 컴포넌트는 단순한 함수로, 리액트에서 함수로서 실행 됨

> **JSX 코드는 React에서 컴포넌트 간의 관계와 UI 구조를 트리 형태로 정의합니다. React는 이 정보를 사용해 ==Virtual DOM==을 생성하고, 최적의 방식으로 실제 DOM을 조작하여 변경 사항을 반영합니다. 즉, JSX는 UI의 상태와 구조를 효율적으로 관리하기 위한 청사진 역할을 하며, React가 필요한 DOM 변경만 수행하도록 돕습니다. 이를 통해 성능을 최적화하고 코드를 직관적으로 작성할 수 있습니다.**
###### 중괄호 변수
- 요소태그 내 동적인 값 할당 가능
- JSX나 요소태그 속성으로도 값 할당 가능
- 따옴표를 제거하고 사용
###### 정적 요소
- <img src="src/assets/react-core-concepts.png" alt="Stylized atom" /> 
	- 요런 식으로 코드를 짜면, 빌드과정에서 파일이 무시되거나 배포 과정에서 유실될 수 있다.
	- 또한 추가적인 최적화 단계를 사용할 수 없음
- import reactImg from '상대경로';
	- **일반적으로 js파일에서는 이미지를 로드하지 않지만, JSX에서는 코드뿐만 아니라 해당 정적인 부분도 같이 로드 함**
###### `props: 속성`
- 데이터를 컴포넌트로 전달하고 그 데이터를 해당 컴포넌트에서 사용
- 컴포넌트 태그 안에 속성같이 넘겨주는 값을 `props`이라고 함
- 컴포넌트의 매개변수로는 `props`하나의 매개변수만 사용 가능
_코딩 TIPS_
- 컴포넌트 노가다 props 노가다 하지말고, JS 스프레드 함수를 적극 활용해라 (...)
```JSX
<CoreConcept title={CORE_CONCEPTS[0].title} description={CORE_CONCEPTS[0].description} image={CORE_CONCEPTS[0].image}/>
<CoreConcept {...CORE_CONCEPTS[1]}/>
```
- 컴포넌트 props를 개폐 중괄호로 받아서 좀 더 간단하게 작성 가능
```JSX
function CoreConcept(props) {
  return(
    <li>
      <img src={props.image} alt={props.title} />
      <h3>{props.title}</h3>
      <p>{props.description}</p>
    </li>
  )
}

function CoreConcept({image, title, description}) {
  return(
    <li>
      <img src={image} alt={title} />
      <h3>{title}</h3>
      <p>{description}</p>
    </li>
  )
}
```
- import './000.css'; 로 특정 컴포넌트에 특정 CSS를 적용 시켜도 해당 컴포넌트에만 제한적으로 적용되지 않는다.(사용하는 페이지에 같은 요소면 적용됨)
- **=={props.children}은 컴포넌트 태그 사이의 내용을 의미한다.==**
###### 이벤트 처리하기
```JSX
/* legacy */
document.querySelector('button').addEventListener('click', () => {

})
/* props */
<button onClick={}>{children}</button>
```
- **props 형태로 이벤트 등록하기**
	- *요소 태그 내에서 `on` 입력 후 `Ctrl + Space`로 메서드 확인*
	- **`함수명()` 등록** 
		- ==JSX가 렌더링될 때 함수가 즉시 실행되어 그 **반환값**이 이벤트 핸들러로 등록됨.== 
		- 보통, 함수 호출 결과를 전달하거나 디버깅용으로 사용됨.
	- **`함수명` 등록** 
		- 함수 참조를 전달하며, 이벤트 발생 시 해당 함수가 실행됨. 
		- 일반적으로 사용되는 방식.
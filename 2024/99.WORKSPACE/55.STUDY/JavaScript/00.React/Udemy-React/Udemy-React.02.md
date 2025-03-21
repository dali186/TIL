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
```JSX
/* 컴포넌트 내부에서 함수 생성 후 등록 */
const TabButton = ({ children, onSelect }) => {
    function handelClick() {
        console.log('Hello World!');
    }    
return (
    <li>
        <button onClick={handelClick}>{children}</button>
    </li>
    );
};
export default TabButton;
/* 컴포넌트 외부에서 props로 함수를 넘겨준 뒤 등록 */
/* 내부 컴포넌트, props에 onSelect가 추가 됨*/
const TabButton = ({ children, onSelect }) => {
return (
    <li>
        <button onClick={onSelect}>{children}</button>
    </li>
    );
};
export default TabButton;
/* 외부 */
  function handleSelect() {
    console.log('Hello World!');
  }
  return(
	  <TabButton onSelect={handleSelect}>Components</TabButton>
  )
```
- 외부에서 넘겨준 props로 함수를 등록하면, 해당 함수가 외부에 있는 요소와 상호작용 할 수 있는 기회가 생긴다.
- 뜬금없이 든 생각이지만, JavaScript가 이렇게 함수를 넘기고 받을 수 있는 이유는... 참조 객체형 언어라서 그렇다 O/X

**이벤트 핸들러를 등록할 때는 `익명함수`, `함수 참조`를 이용해야 한다.**
```Javascript
/* 익명함수로 이벤트 등록 (포인터를 등록한다) */
<TabButton onSelect={() => handleSelect('components')}>Components</TabButton>
```
- 익명 함수는 이벤트가 발생했을 때 실행되며, 이 함수 내부에서 `handleSelect('components')`를 호출
	- 결과적으로 `handleSelect('components')`는 이벤트가 발생할 때 실행
```Javascript
/* 함수를 이벤트로 등록 */
<TabButton onSelect={handleSelect('components')}>Components</TabButton>
```
- JSX가 렌더링 될 때 즉시 실행 -> 반환값이 onSelect에 저장된다.
	- 이 경우, `handleSelect`가 반환하는 값(`undefined`인 경우가 많음)이 이벤트 핸들러로 등록되기 때문에, 클릭 이벤트가 발생해도 동작하지 않음.
###### 이벤트 실행 후 UI 업데이트
> **UI를 업데이트 하려면 컴포넌트 자체가 업데이트 되어야 한다.**

변수를 지정하고 함수 실행 시 값을 변경하도록 설정 -> 값은 변경되나(script는 실행 되나) UI가 업데이트 되지 않음.
- ==컴포넌트 내부의 이벤트 함수가 실행되었더라도, 컴포넌트 자체 함수가 다시 실행되지 않으면 JSX코드가 재평가 되지 않음(재렌더링 하지 않음).==
	- React는 **Virtual DOM**을 활용하여, JSX 코드의 결과를 현재 UI와 비교(diffing)한 후 필요한 부분만 업데이트
	- 컴포넌트가 다시 렌더링되지 않으면 React는 diffing을 수행하지 않으므로, UI 업데이트도 이루어지지 않음

#### 상태관리와 훅(Hook)
> React에게 데이터가 변경되었다는 것을 알리고, UI를 업데이트 시켜주기 위한 목적의 리액트 라이브러리 함수
- `use`로 시작되는 모든 함수는 `React Hook`
- **일반 함수이지만, React 컴포넌트 함수 또는 다른 React Hook 안에서 호출되어야 함.**
- 컴포넌트 함수 최상위에서 호출
- 데이터가 변경되면 이 Hook이 자신이 속한 컴포넌트 함수를 활성화하여 재렌더링을 시도.
```Javascript
const [ selectedTopic, setSelectedTopic ] = userState('Please click a button');
```
- useState에서 반환 된 첫번째 요소(selectedTopic) = 컴포넌트 실행 주기의 현재 데이터 스냅샷
	- 컴포넌트 함수가 처음 실행될 때 이 초기 값이 selectedTopic에 저장됨
	- 다시 실행될 때에는 업데이트 된 값이 저장됨
- useState에서 반환 된 두번째 요소(setSelectedTopic) = 리액트에서 제공되는 함수, 저장된 값(스냅샷)을 업데이트 해주는 함수
	- 해당 함수가 실행되면, React에게 이 컴포넌트 함수를 다시 실행해야 함을 알림
- *useState로 상태를 업데이트 했어도 로그를 출력하면 상태를 변경하기 전의 상태 값이 나온다.*

**분기처리 코드 깔끔하기 갈기기**
1. 삼항연산자 사용
```Javascript
!selectedTopic ? (
            <p>Please select a topic.</p>
          ) : (
            <div id='tab-content'>
            <h3>{EXAMPLES[selectedTopic].title}</h3>
            <p>{EXAMPLES[selectedTopic].description}</p>
            <pre>
              <code>
              {EXAMPLES[selectedTopic].code}
              </code>
            </pre>
          </div>
          )} 
```
2. && 연산자 사용
```Javascript
{!selectedTopic && <p>Please select a topic.</p>}
          {selectedTopic && (
            <div id='tab-content'>
            <h3>{EXAMPLES[selectedTopic].title}</h3>
            <p>{EXAMPLES[selectedTopic].description}</p>
            <pre>
              <code>
              {EXAMPLES[selectedTopic].code}
              </code>
            </pre>
          </div>
          )}
        </section>
      </main>
    </div>
```
3. 변수에 JSX 담아서 사용
	- 미리 JS코드에서 if분기 등 처리 후에 깔끔하게 return문에 집어 넣어줄 수 있음
###### css 적용하기
React에서는 클래스이름을 설정하기 위해 `className` prop를 사용한다. (id, name 등은 html과 동일하다)

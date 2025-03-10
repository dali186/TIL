React 기반, Front-end 뿐만 아니라 Server의 기능 수행.
`let`은 블록 내에 서만 사용 가능.
`var`는 해당 변수가 포함된 블록까지 사용 가능.

npx sb@latest init
npm run storybook

##### Static Site Generation(SSG)
1. 빌드 시 `getStaticProps` 함수 호출
2. 함수 내에서 API 호출 등을 수행
3. 페이지를 그리는데 필요한 props를 반환
4. 빌드 결과는 정적 파일의 형태로 저장
5. 페이지 접근 시 저장된 파일을 클라이언트에게 전송
> 초기화면 그리기가 빠르지만 빌드시에만 데이터를 얻으므로 실시간성 콘텐츠에는 적합하지 않음

##### Client Side Rendering(CSR)
1. 브라우저에서 초기 화면을 그린 뒤
2. 비동기로 데이터를 얻어서 데이터를 표시
> SEO가 유효하지 않음

##### Server Side Rendering(SSR)
1. 페이지 접근이 발생할 때 마다 `getServerSideProps` 함수 호출
2. 접근 시 마다 서버에서 데이터를 가져와서 화면을 그림
> 최신 데이터를 표시하고자 하는 경우에 적합

##### Incremental Static Regeneration
SSG의 응용.
사전에 페이지를 생성 + 접근이 발생함에 따라 페이지를 다시 생성

###### 정적 컨텐츠로 전송할 수 있는 부분은 빌드할 때 생성(SSG)
###### 개별 컨텐츠에 관해서는 클라이언트 사이드에서 API를 사용해 정적으로 페이지 표시(CSR)
SSR은 사용자별로 HTML을 생성해야하므로 대량의 HTML을 캐싱하기 어려움

###### SPA(Single Page Application)
AS-IS: 서버에서 HTML을 생성하고 UI 구성하여 클라이언트에게 전송
TO-BE: 서버에서 HTML을 생성하고 클라이언트에게 전송 후 UI 구성

### 컴포넌트
###### 아토믹 디자인
###### 프레젠테이션 컴포넌트
: props 데이터 할당, 스타일 지정 / 기능 정의 X
###### 컨테이너 컴포넌트
: 디자인은 구현하지 않고 비즈니스 로직만 담당
: Hooks를 가짐


화살표 함수의 명시적 반환(Explicit Return)과 암시적 반환(Implicit Return)
###### 암시적 반환
화살표 함수에서 중괄호 `{}`를 생략하면, **암시적으로** `return`이 포함됩니다. 따라서 `return`을 명시적으로 작성하지 않아도 값을 반환할 수 있습니다.
```Javascript
const Logo = () => (
    <a className="gh-head-logo" href="/">
        <img src="/images/logo.png" alt="MainLogo" className="h-8" />
    </a>
);
```
###### 명시적 반환
만약 함수 본문이 여러 줄로 이루어져 있거나, 추가 로직이 필요하다면 중괄호 `{}`를 사용하고, `return`을 명시적으로 작성해야 합니다.
```Javascript
const Logo = () => {
    return (
        <a className="gh-head-logo" href="/">
            <img src="/images/logo.png" alt="MainLogo" className="h-8" />
        </a>
    );
};
```
##### TailwindCSS는 동적으로 생성한 CSS를 제거한다.
- 개발자 도구로 확인한 HTML에는 클래스에 그대로 박혀있는데, CSS가 적용되지 않음.
- 
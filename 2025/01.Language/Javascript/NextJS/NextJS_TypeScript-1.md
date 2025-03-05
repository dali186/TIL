[NextJS 프로젝트 구조 설정](https://hotsunchip.tistory.com/12)
Dynamic Route
[NextJS doc](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes)
 [locale] 폴더를 만들어 이 폴더 하위에 페이지들을 관리하면, 앞에 en / ja / ko 등을 붙였을 때 텍스트는 다르지만 레이아웃은 같도록 할 수 있다.

03/01(토)
- SSR, SSG 그리고 CSR의 차이점
- SSG의 도입 필요성
	- CSR(클라이언트 사이드 렌더링)의 경우에는 첫 페이지 로드 시의 딜레이가 큰 단점이다.
	- 서버에서 HTML을 만들고 클라이언트에서 전송, 클라이언트는 JS로 UI를 구성한다. (딜레이 발생)
- SSR(서버사이드 렌더링)
	- 서버에서 HTML을 만들고 UI를 구성하여 클라이언트에게 전달
	- 빠르지만, 서버의 부하가 크다.
- SSG(스태틱 사이트 제너레이션)
	- SSR은 사용자 요청 시에 HTML생성 및 구성하여 전달하지만, SSG는 애초에 빌드시에 생성된다.
	- 캐싱가능(CDN)
- NextJS는 SSR과 SSG를 조합하여 사용한다. (정적인 페이지에 경우는 SSG가 효율적이다.)
- BBD(## **Behavior Driven Development**, 잘 짠 TDD)는 TDD의 한 종류이다.
- (Spring) QueryDSL 설정

03/04(화)
**목표**
- React 동작과정
- React Hooks
- React Context
03/05(수)
React:state
- **시간이 지나도 변하지 않나요?** 그러면 확실히 state가 아닙니다.
- **부모로부터 props를 통해 전달됩니까?** 그러면 확실히 state가 아닙니다.
- 컴포넌트 안의 다른 state나 props를 가지고 **계산 가능한가요?** 그렇다면 _절대로_ state가 아닙니다!

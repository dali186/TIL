1. **React 프로젝트를 시작하는 방법**
	```
	- (브라우저) react.new
	- npm create vite@lastest react-project
	- npm create-react-app react-project
	```
- [Deno란](https://kdydesign.github.io/2022/02/17/deno-tutorial/)
	Deno는 TypeScript와 JavaScript 실행을 지원하는 새로운 런타임으로, Node.js의 대안으로 설계되었습니다. 보안이 기본적으로 강화되어 있으며, 최신 ES 모듈 시스템과 간단한 코드 포맷팅 및 테스트 기능을 제공합니다. Node.js와는 달리 패키지 관리자가 필요 없으며 URL을 통해 외부 모듈을 가져옵니다.
- [Capacitor란](https://capacitorjs.com/)
	크로스 플랫폼 네이티브 런타임입니다. 웹 기술(HTML, CSS, JavaScript)을 사용하여 모바일, 데스크톱, 웹 애플리케이션을 제작할 수 있도록 하며, 네이티브 기능(카메라, 파일 시스템 등)을 호출할 수 있습니다. Cordova와 유사하지만 더 현대적이고 확장 가능한 설계를 제공하며, 네이티브 프로젝트를 직접 수정하거나 기존의 웹 앱을 네이티브 앱으로 변환하는 데 유리합니다.
2. **Basic Javascript** 
- JavaScript를 사용하는 법
	- HTML 코드에 <script></script>를 추가 (사용 X)
	- .js 파일을 HTML 코드에 import
		- defer
		- type="module"
			- js 파일을 모듈로 취급할 경우, import/export 문법을 사용 가능
- ==React는 프로세스를 활용, 해당 과정에서 HTML 코드에 자동으로 script 태그를 추가해준다.(컴포넌트 스캔 그런 느낌일까...)==
3. **React코드에는 script 태그 없이 동작하는 이유**
	- 기존 HTML + Vanilla.js의 경우, 서버가 HTML 문서를 제공하고, 클라이언트(브라우저)가 JavaScript를 실행하여 동적 요소를 처리
	- React의 경우, JSX(JavaScript XML)으로 작성되고, 빌드 시 해당 코드들이 JavaScript로 변환 후 브라우저에서 실행(react-scripts 패키지)
	- ==결과적으로, React 애플리케이션은 컴파일된 JavaScript로 동작하므로, HTML 내에 `<script>` 태그를 직접 추가할 필요가 없습니다.==
4. **React가 빌드 프로세스 과정을 거쳐야하는 이유**
	- 처리되지 않은 리액트 코드는 브라우저에서 실행 불가
		- JSX코드는 HTML 요소가 가미되어 있는데, 이 문법은 js 런타임에서 실행 할 수 없다.
	- 작성된 코드가 프로덕션을 위해 최적화되지 않았기 때문
		- 코드 최적화 및 간소화가 되어 있지 않아, 배포 시 불필요한 내용까지 추가되기 때문

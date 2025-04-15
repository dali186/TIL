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
	```Javascript
	const userNameData = ["Max", "Schwarzmuller"];
	const [firstName, lastName] = ["Max", "Schwarzmuller"];

	const user = {
		name: "Max",
		age: 34
	};
	/* 동일한 프로퍼티 명 사용해야 함 */
	const {name, age} = {
		name: "Max",
		age: 34
	};
	/* 혹은 별칭 추가*/
	const {name: userName, age} = {
		name: "Max",
		age: 34
	};
	```
	- `...` : 배열의 모든 원소를 가져온다.
	- **함수의 매개변수로 함수가 들어갈 때**
		- 소괄호가 존재 : 매개변수 함수의 결과 값이 해당 함수로 전달된다.
		- 소괄호가 부재 : 콜백 함수로 사용된다. (해당 함수가 끝나면 매개변수 함수 실행 시작)
	- Array Functions
		- `map()`  => [map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
		- `find()`  => [find](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
		- `findIndex()`  => [findIndex](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)  
		- `filter()`  => [filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)  
		- `reduce()`  => [Reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce?v=b)  
		- `concat()`  => [concat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat?v=b)  
		- `slice()`  => [slice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)  
		- `splice()`  => [splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
3. **React코드에는 script 태그 없이 동작하는 이유**
	- 기존 HTML + Vanilla.js의 경우, 서버가 HTML 문서를 제공하고, 클라이언트(브라우저)가 JavaScript를 실행하여 동적 요소를 처리
	- React의 경우, JSX(JavaScript XML)으로 작성되고, 빌드 시 해당 코드들이 JavaScript로 변환 후 브라우저에서 실행(react-scripts 패키지)
	- ==결과적으로, React 애플리케이션은 컴파일된 JavaScript로 동작하므로, HTML 내에 `<script>` 태그를 직접 추가할 필요가 없습니다.==
4. **React가 빌드 프로세스 과정을 거쳐야하는 이유**
	- JSX 코드 실행 불가(*JavaScript 런타임에서 HTML 요소 실행 불가*)
		- JSX는 JavaScript 문법에 HTML 요소가 포함된 형태로 작성됩니다. 브라우저의 JavaScript 엔진은 JSX를 직접 실행할 수 없으므로, 빌드 도구(Babel 등)를 사용해 JSX를 표준 JavaScript로 변환해야 합니다.
	- 프로덕션 최적화 필요
		- React 개발 환경에서는 디버깅 도구, 주석, 그리고 불필요한 코드를 포함한 상태로 작성됩니다. 빌드 과정에서 코드를 압축하고 최적화하여 파일 크기를 줄이고 성능을 개선하여 프로덕션 배포에 적합하게 만듭니다.
5. **Export/Import**
	Vanilla JS에서는 스크립트 추가 시, type="module"을 지정해 주어야 함    
	React는 빌드 프로세스가 import와 export 키워드가 있는 개별 파일을 모두 합쳐 하나의 큰 파일을 만든 다음 기존 문법을 순서대로 사용해 import 구문 처리    
		-> 브라우저가 **여러 개의 작은 JS파일**을 다운로드 하는 대신 **몇 개의 큰 JS파일**만 다운로드 하면 되므로 효율적임     
		-> import/export 문법을 지원하지 않는 브라우저에서도 사용이 가능하게 됨
	- Export
		- 변수 및 함수: 변수 앞에 export 예약어를 사용.
		- default 예약어는 파일 당 하나만 존재할 수 있음(익명 함수, 변수도 사용 가능)
	- Import
		- 변수 및 함수: import { 변수명 및 함수명 } from "파일(상대)경로" (확장자 없어도 됨, 빌드 시 알아서 추가)
		- default: import 변수명 from "파일(상대)경로"
		- import * as 별칭 from "파일(상대)경로", 이런 식으로 한 파일의 여러 모듈을 import 가능
		- import { export변수1, export함수1 as abc } from "파일(상대)경로", 이런 식으로도 import 가능
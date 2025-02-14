JavaScript를 테스트할 수 있는 툴: `Jest(React)`, `Cypress`, `Mocha`...
### Cypress
[Cypress](https://www.cypress.io/) 테스트 결과를 시각적으로 확인할 수 있음.
###### Getting Start
	* `npm install cypress -D`
	* `npx cypress open`
1. Cypress 실행
2. project upload
3. config 생성
4. `spec.cy.js` 파일 생성 -> 테스트 코드를 정의하는 파일

##### Cypress 문법
###### 구조
1. **`describe()`** : 테스트 코드를 묶는 가장 큰 단위, Test Suite
2. **`context()`** : describe()와는 기능적차이가 없음. 의미적으로 구분하기 위해 사용
3. **`it()`** : 실제 테스트를 정의하는 함수
###### Hook
1. **`before()`** : Test Suite의 **첫 번째 테스트 케이스가 실행되기 전**에 한번만 실행.
2. **`after()`** : Test Suite의 **마지막 테스트 케이스가 실행된 후에** 한번만 실행.
3. **`beforeEach()`** : Test Suite의 **각 테스트 케이스가 실행되기 전**에 한번만 실행.
4. **`afterEach()`** : Test Suite의 **각 테스트 케이스가 실행된 후**에 한번만 실행.
###### Assertion
> 비동기적으로 동작하며 조건이 만족할 때까지 대기, 체이닝 가능.

- get
- should
- its
- and
- or
- cy.window()
- cy.wrap()
###### boilerPlate 설정
- `cypress > support > commands.js`
```javascript
Cypress.Commands.add('login', (email, password) => {
  cy.get('input[name=email]').type(email);
  cy.get('input[name=password]').type(password);
  cy.get('form').submit();
});
```
###### cypress.config.js
- e2e
	- viewportWidth
	- viewportHeight
	- pageLoadTimeout
	- chromeWebSecurity: false
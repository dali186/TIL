[Reference:TypeScript](https://www.typescriptlang.org/ko/docs/handbook/intro.html)
[Reference:JavaScript](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide)
TypeScript는 JS의 구문이 허용되는, JavaScript의 _상위 집합_ 언어입니다.
TypeScript는 JavaScript의 _런타임 특성_을 가진 프로그래밍 언어
TypeScript는 추가 런타임 라이브러리를 제공하지 않습니다.
```shell
npm install -g typescript
tsc ${파일명.ts}
```

**코드에 대한 타입 검사는 프로그램이 실행할 수 있는 동작을 제한**
Javascript에서 실행되는 코드인데, Type제한으로 인해 오류가 발생할 경우, TypeScript가 방해하지 못하게 하도록 컴파일 단계에서 오류가 나도 js로는 컴파일 진행됨.
*엄격하게 컴파일* `tsc --noEmitOnError`

###### 변수 type 명시하기
```TypeScript
function greet(person: string, date: Date) {
	console.log(`Hello ${person}, today is ${date.toDateString()}!`);
}
```
TypeScript가 변수 타입을 추론가능 
> 타입 시스템이 알아서 올바른 타입을 어떻게든 잘 알아낼 수 있다면 타입 표기를 굳이 적지 않는 것이 가장 좋습니다.

TypeScipt 작성 -> 컴파일 -> JsCode 반환 
※ **기억하세요**: 타입 표기는 프로그램의 런타임 동작을 전혀 수정하지 않습니다.

 TypeScript는 새 버전의 ECMAScript의 코드를 ECMAScript 3 또는 ECMAScript 5와 같은 보다 예전 버전의 것들로 다시 작성해 줍니다. 새로운 또는 “상위” 버전의 ECMAScript를 예전의 또는 “하위” 버전의 것으로 바꾸는 과정을 _다운레벨링_이라 부르기도 합니다.

_`--target` 플래그를 설정하면 보다 최근 버전을 타겟으로 변환을 수행할 수도 있습니다. `--target es2015`를 실행_

**엄격도**
 CLI에서 `--strict` 플래그를 설정하거나 [`tsconfig.json`](https://www.typescriptlang.org/ko/docs/handbook/tsconfig-json.html)에 `"strict": true`를 추가하면 모든 플래그를 동시에 활성화하게 되지만, 각각의 플래그를 개별적으로 끌 수도 있습니다. 반드시 알아야 하는 두 가지 가장 주요한 옵션은 `noImplicitAny`와 `strictNullChecks`입니다.
- noImplicitAny
	- `noImplicitAny` 플래그를 활성화하면 타입이 `any`로 암묵적으로 추론되는 변수에 대하여 오류를 발생
- strictNullChecks
	- `strictNullChecks` 플래그는 `null`과 `undefined`를 보다 명시적으로 처리하며, `null` 및 `undefined` 처리를 _잊었는지_ 여부를 걱정하는 데에서 우리를 _해방시켜_ 줍니다.

##### Type
###### 1. 원시타입
- **`String`**
- **`Number`**
	- JavaScript는 정수를 위한 런타임 값을 별도로 가지지 않으므로, `int` 또는 `float`과 같은 것은 존재하지 않습니다. 모든 수는 단순히 `number`입니다
- **`boolean`**
###### 2. 배열
###### 3. any

##### 타입표기
###### 1. 변수
```TypeScript
let myName: string = "Alice";
```
TypeScript는 `int x = 0;`과 같이 “타입을 왼쪽에 쓰는” 식의 표기법을 사용하지 않습니다. 타입 표기는 항상 타입의 대상 _뒤쪽에_ 위치합니다.

_하지만 대부분의 경우, 타입 표기는 필요하지 않습니다. 가능하다면 TypeScript는 자동으로 코드 내의 있는 타입들을 _추론_하고자 시도합니다. 예를 들어, 변수의 타입은 해당 변수의 초깃값의 타입을 바탕으로 추론됩니다._

###### 2. 함수
매개변수 타입 표기
```TypeScript
function greet(name: string) {
	console.log("Hello, " + name.toUpperCase() + "!!");
}
```
반환 타입 표기
```TypeScript
function getFavoriteNumber(): number {
	return 26;
}
```

**익명 함수는 함수 선언과는 조금 다릅니다. 함수가 코드상에서 위치한 곳을 보고 해당 함수가 어떻게 호출될지 알아낼 수 있다면, TypeScript는 해당 함수의 매개 변수에 자동으로 타입을 부여**

##### 객체 타입
```TypeScript
// 매개 변수의 타입은 객체로 표기되고 있습니다.
function printCoord(pt: { x: number; y: number }) {
	console.log("The coordinate's x value is " + pt.x);
	console.log("The coordinate's y value is " + pt.y);
}
printCoord({ x: 3, y: 7 });
```

##### 옵셔널 프로퍼티
객체 타입은 일부 또는 모든 프로퍼티의 타입을 선택적인 타입, 즉 _옵셔널_로 지정할 수 있습니다. 프로퍼티 이름 뒤에 `?`를 붙이면 됩니다.

```TypeScript
function printName(obj: { first: string; last?: string }) {
	// ...  
	}  
	// 둘 다 OK  
	printName({ first: "Bob" });  
	printName({ first: "Alice", last: "Alisson" });   
```
JavaScript에서는 존재하지 않는 프로퍼티에 접근하였을 때, 런타임 오류가 발생하지 않고 `undefined` 값을 얻게 됩니다. **이 때문에 옵셔널 프로퍼티를 _읽었을_ 때, 해당 값을 사용하기에 앞서 `undefined`인지 여부를 확인해야 합니다.**

### 유니언 타입 정의하기

타입을 조합하는 첫 번째 방법은 _유니언_ 타입을 사용하는 것입니다. 유니언 타입은 서로 다른 두 개 이상의 타입들을 사용하여 만드는 것으로, 유니언 타입의 값은 타입 조합에 사용된 타입 중 _무엇이든 하나_를 타입으로 가질 수 있습니다. 조합에 사용된 각 타입을 유니언 타입의 _멤버_라고 부릅니다.

문자열 또는 숫자를 받을 수 있는 함수를 작성해보겠습니다.

`   function printId(id: number | string) {    console.log("Your ID is: " + id);  }   `

TypeScript는 오직 `string` 값만이 `typeof` 연산의 결괏값으로 `"string"`을 가질 수 있다는 것을 알고 있습니다.
```TypeScript
function printId(id: number | string) {
	if (typeof id === "string") {
	// 이 분기에서 id는 'string' 타입을 가집니다
	console.log(id.toUpperCase());
	} else {
	// 여기에서 id는 'number' 타입을 가집니다
	console.log(id);
	}
}
```

##### 타입 별칭
똑같은 타입을 한 번 이상 재사용하거나 또 다른 이름으로 부르고 싶은 경우도 존재합니다.

_타입 별칭_은 바로 이런 경우를 위하여 존재하며, _타입_을 위한 _이름_을 제공합니다. 타입 별칭의 구문은 아래와 같습니다.
```TypeScript
type Point = {
	x: number;
	y: number;
};
// 앞서 사용한 예제와 동일한 코드입니다
function printCoord(pt: Point) {
	console.log("The coordinate's x value is " + pt.x);
	console.log("The coordinate's y value is " + pt.y);
}
printCoord({ x: 100, y: 100 });
```


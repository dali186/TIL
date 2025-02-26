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
###### 원시타입
- **`String`**
- **`Number`**
	- 
- **`boolean`**

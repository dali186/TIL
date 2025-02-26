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


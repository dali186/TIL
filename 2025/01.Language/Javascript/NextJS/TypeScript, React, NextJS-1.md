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
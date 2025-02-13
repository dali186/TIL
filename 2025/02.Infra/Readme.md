### ReverseProxy와 Proxy
##### Foward Proxy
- `Client`바로 앞 단에 위치
	- Client 요청이 Internet으로 가기 전 처리 가능
	- Server는 Client의 정보를 모른다
		- IP 우회 및 익명성 유지
		- 캐싱 기능
		- 특정 사이트 차단
##### Reverse Proxy
- `Server`바로 앞 단에 위치
	- Server 응답이 Internet으로 가기 전 처리 가능
	- Client는 Server의 정보를 모른다(Proxy 정보로 대체)
		- 로드 밸런싱
		- SSL 종료
		- 보안 강화
		- 캐싱

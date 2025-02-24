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

### MSA
- API를 통해서만 상호작용
	- 외부는 API만을 알 수 있고, 내부는 추상화가 되어있다
- SOA
- REST 등 가벼운 통신 아키텍처, 또는 Kafka 등을 이용한 message stream을 주로 사용
- 각각의 서비스는 모듈화가 되어있으며 이러한 모듈까리는 RPC 또는 message-driven API등을 이용하여 통신

### Windows 외부 DNS 제거
Get-NetIPConfiguration
Get-DnsClientServerAddress
Set-DnsClientServerAddress -InterfaceAlias "Wi-Fi" -ResetServerAddresses

### CI/CD용 SSH 키 생성
1. ssh-keygen -t rsa -b 4096 -C "nnagicarp@gmail.com"
2. cat ~/.ssh/id_rsa.pub
3. cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
4. 

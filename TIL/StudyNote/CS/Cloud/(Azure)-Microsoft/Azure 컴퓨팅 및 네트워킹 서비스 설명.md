[Ref 1. Link #1](https://learn.microsoft.com/ko-kr/training/modules/describe-azure-compute-networking-services/1-introduction)
[Ref 2. Link #1](https://learn.microsoft.com/ko-kr/training/modules/describe-core-architectural-components-of-azure/)

## #1 Azure VM이란
---
##### Azure VM(가상머신) 사용 목적
- OS(운영 체제)에 대한 완전한 제어
- 사용자 지정 소프트웨어를 실행하는 기능
- 사용자 지정 ==호스팅 구성을 사용==해야 하는 경우
##### Azure VM(가상머신) 사용 예시
- 테스트 및 개발 진행 시
- 클라우드에서 애플리케이션을 실행하는 경우
- 클라우드로 데이터 센터 확장 시
- 재해 복구 시
##### VM(가상머신) 리소스
- 크기(용도, 프로세스 코어 수 및 RAM 양)
- 스토리지 디스크(HDD, SSD 등)
- 네트워킹(==**가상 네트워크**, **공용 IP 주소 및 포트 구성**==)
#### 실습 코드
---
***Azure Portal이 아닌, Azure CLI 사용하여 구축***
#### 1. Linux 가상 머신 만들기 및 Nginx 설치
##### 1-1. 가상 머신 만들기
```
az vm create 
--resource-group "learn-061d12b5-46ed-4fb4-b126-396c87f50d4f" 
--name my-vm 
--public-ip-sku Standard 
--image Ubuntu2204 
--admin-username azureuser 
--generate-ssh-keys
```
###### `vm create` 명령어 options
- `resource-group` : 리소스 그룹, AzurePortal에서 Sandbox 계정 전환 후 발급받아왔음
- `name` : vm 이름
- `public-ip-sku` : Standard, [Ref 2. SKU in Azure](https://learn.microsoft.com/ko-kr/azure/virtual-network/ip-services/public-ip-addresses)
- `image` : OS 지정
- `admin-username` : hostusername
- `generate-ssh-keys` : SSH키 발급, ~~이거 .pem으로 안 떨어지나?~~
##### 1-2. Result
```
{
  "fqdns": "",
  "id": "/subscriptions/66934742-a2f4-4f94-ad7b-07a47d83d2bc/resourceGroups/learn-061d12b5-46ed-4fb4-b126-396c87f50d4f/providers/Microsoft.Compute/virtualMachines/my-vm",
  "location": "westus",
  "macAddress": "00-0D-3A-31-AC-20",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "104.40.66.156",
  "resourceGroup": "learn-061d12b5-46ed-4fb4-b126-396c87f50d4f",
  "zones": ""
}
```
- `macAddress`, `privateIpAddress`, `publicIpAddress`가 발급됐다.
##### 2-1. 가상머신에서 Nginx 구성
```
az vm extension set 
--resource-group "learn-061d12b5-46ed-4fb4-b126-396c87f50d4f" 
--vm-name my-vm --name customScript 
--publisher Microsoft.Azure.Extensions 
--version 2.1 
--settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"]}' 
--protected-settings '{"commandToExecute": "./configure-nginx.sh"}'
```
###### `vm extension set` 명령어 options
- `resource-group`
- `vm-name`
- `name` : Extension 이름
- `publisher` : Extension을 제공하는 Publisher
- `version`
- `settings` : 사용자 지정(Github에 저장되어 있는) 스크립트를 VM에 다운로드
- `protected-settings` : `commandToExcute` 명령어로 스크립트 실행

## #2 Azure 가상 네트워킹 
---
##### Azure 가상 네트워킹
**Azure 가상 네트워크가 제공하는 기능**
- 격리 및 구분
- 인터넷 통신
- Azure 리소스 간 통신
- 온-프레미스 리소스와 통신
- 네트워크 트래픽 라우팅
- 네트워크 트래픽 필터링
- 가상 네트워크 연결
> Azure 가상 네트워킹은 퍼블릭 엔드포인트(공인 IP), 프라이빗 엔드포인트(사설 IP)를 모두 지원

#### 실습 코드 - 네트워크 액세스 구성
---
***Azure Portal이 아닌, Azure CLI 사용하여 구축***
#### 1. 웹 서버 엑세스
##### 0. 실행중인 VM 확인
```
az vm list
```
##### 1-1. VM의 IP 주소를 가져오고 결과를 Bash 변수로 저장
```
IPADDRESS=
"$(az vm list-ip-addresses 
--resource-group "learn-9257009b-4cb4-4d64-be74-c7e623afc79b" 
--name my-vm 
--query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" 
--output tsv)"
```
##### 1-2. `curl` 명령어로 홈페이지 다운로드
```
curl --connect-timeout 5 http://$IPADDRESS

# Result
curl: (28) Connection timed out after 5001 milliseconds
# IP 주소 출력
echo $IPADDRESS
```
- 제한 시간 (5s) 내에 엑세스 불가
- `echo $IPADDRESS` 명령어 결과: 52.160.107.119
	- 해당 IP를 웹 브라우저로 접속해도 실패
#### 2. 현재 네트워크 보안 그룹 규칙 확인
##### 2-1. 현재 네트워크 보안 그룹 규칙 나열
```
az network nsg list 
--resource-group "learn-9257009b-4cb4-4d64-be74-c7e623afc79b" 
--query '[].name' 
--output tsv

# Result
my-vmNSG
```
- Azure의 각 VM은 **하나 이상의 네트워크 보안 그룹에 연결**
- 내가 생성한 vm은 `my-vmNSG`라는 네트워크 보안 그룹를 생성 후 연결
- `az network nsg list`
	- `resource-group`
	- `query`
	- `output`
##### 2-2. 현재 네트워크 보안 그룹 규칙 나열
```
az network nsg rule list 
--resource-group "learn-9257009b-4cb4-4d64-be74-c7e623afc79b" 
--nsg-name my-vmNSG

# Result
[
  {
    "access": "Allow",
    "destinationAddressPrefix": "*",
    "destinationAddressPrefixes": [],
    "destinationPortRange": "22",
    "destinationPortRanges": [],
    "direction": "Inbound",
    "etag": "W/\"0aeddee4-9dc3-4415-a88a-c7cdef49da20\"",
    "id": "/subscriptions/66934742-a2f4-4f94-ad7b-07a47d83d2bc/resourceGroups/learn-9257009b-4cb4-4d64-be74-c7e623afc79b/providers/Microsoft.Network/networkSecurityGroups/my-vmNSG/securityRules/default-allow-ssh",
    "name": "default-allow-ssh",
    "priority": 1000,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "learn-9257009b-4cb4-4d64-be74-c7e623afc79b",
    "sourceAddressPrefix": "*",
    "sourceAddressPrefixes": [],
    "sourcePortRange": "*",
    "sourcePortRanges": [],
    "type": "Microsoft.Network/networkSecurityGroups/securityRules"
  }
]
```
- `az network nsg rule list`
	- `resourcce-group`
	- `nsg-name ${내 nsg 이름}`
**좀 더 보기 쉽게**
```
az network nsg rule list 
--resource-group "learn-9257009b-4cb4-4d64-be74-c7e623afc79b" 
--nsg-name my-vmNSG 
--query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}' 
--output table

Name               Priority    Port    Access
-----------------  ----------  ------  --------
default-allow-ssh  1000        22      Allow
```
- 기본 규칙인 _default-allow-ssh_가 표시_
	- 해당 규칙은 포트 22(SSH)를 통한 인바운드 연결을 허용
- option `query`, `output` 추가
#### 2. 현재 네트워크 보안 그룹 규칙 만들기
##### 2-1. 현재 네트워크 보안 그룹에 80(HTTP) 허용하는 규칙 생성
```
az network nsg rule create 
--resource-group "learn-9257009b-4cb4-4d64-be74-c7e623afc79b" 
--nsg-name my-vmNSG 
--name allow-http 
--protocol tcp 
--priority 100 
--destination-port-range 80 
--access Allow

# Result
{
  "access": "Allow",
  "destinationAddressPrefix": "*",
  "destinationAddressPrefixes": [],
  "destinationPortRange": "80",
  "destinationPortRanges": [],
  "direction": "Inbound",
  "etag": "W/\"df654edd-b5ed-4561-aaa3-05dfc4f6395e\"",
  "id": "/subscriptions/66934742-a2f4-4f94-ad7b-07a47d83d2bc/resourceGroups/learn-9257009b-4cb4-4d64-be74-c7e623afc79b/providers/Microsoft.Network/networkSecurityGroups/my-vmNSG/securityRules/allow-http",
  "name": "allow-http",
  "priority": 100,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "learn-9257009b-4cb4-4d64-be74-c7e623afc79b",
  "sourceAddressPrefix": "*",
  "sourceAddressPrefixes": [],
  "sourcePortRange": "*",
  "sourcePortRanges": [],
  "type": "Microsoft.Network/networkSecurityGroups/securityRules"
}
```
- `az network nsg rule create`
##### 2-2. 생성된 규칙 확인
```
az network nsg rule list 
--resource-group "learn-9257009b-4cb4-4d64-be74-c7e623afc79b" 
--nsg-name my-vmNSG 
--query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}' 
--output table

Name               Priority    Port    Access
-----------------  ----------  ------  --------
default-allow-ssh  1000        22      Allow
allow-http         100         80      Allow
```
- `az network nsg rule list`


[Ref 1. Link](https://learn.microsoft.com/ko-kr/training/modules/describe-azure-compute-networking-services/1-introduction)
### #1 Azure VM이란
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
###### `vm extension` 명령어 options
- `resource-group` : 리소스 그룹, AzurePortal에서 Sandbox 계정 전환 후 발급받아왔음
- `name` : vm 이름
- `public-ip-sku` : Standard, [Ref 2. SKU in Azure](https://learn.microsoft.com/ko-kr/azure/virtual-network/ip-services/public-ip-addresses)
- `image` : OS 지정
- `admin-username` : hostusername
- `generate-ssh-keys` : SSH키 발급, ~~이거 .pem으로 안 떨어지나?~~
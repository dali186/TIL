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
```
az vm create 
--resource-group "learn-061d12b5-46ed-4fb4-b126-396c87f50d4f" 
--name my-vm 
--public-ip-sku Standard 
--image Ubuntu2204 
--admin-username azureuser 
--generate-ssh-keys

```

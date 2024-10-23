
#### TIPS
---
[Azure 학습](https://learn.microsoft.com/ko-kr/training/azure/) _keyWord: "만들기"_
### 학습내용
---
##### 클라우드 아키텍처
**`서비스 오케스트레이션`**
	자동화된 리소스 프로비저닝
	리소스 배치를 자동하기 위한 설정, 관리, 조정 작업
`클라우드 서비스 관리`
	경영 지원, 프로비저닝/구성, 이식성/상호 운영성
`클라우드 아키텍처링`
	클라우드 서비스 설계(오케스트레이션, 비용 고려)
	리스크 분석, 리소스 배치
**효율성과 가용성을 높이는 아키텍처**
1. **==리소스 풀링==**
2. ==**로드 밸런싱**==
3. ==**오토 스케일링**==
4. ==**클라우드 버스팅**==
**고가용성(HA: High Availability)
- 서버와 네트워크, 프로그램 등의 시스템이 오랜 기간 동안 지속적으로 정상 운영이 가능한 특성
	- `다중 애플리케이션 서버와 부하 **분산**`
	- `데이터베이스 혹은 스토리지 이중화`
	- `여러 지리적 위치에 따른 서비스 배치`
#### 리소스 풀링
**`리소스 풀`** : 서버, 스토리지 등 리소스를 담아 두는 공간 (H/W)
	- 물리적 위치를 알 수 없다(IDC의 특정 서버, 스토리지 내부의 지리적 위치 등)
	- 사용이 용이하도록 추상화
	- 서비스나 프로그램에 의하여 자유롭게 사용되고 해제
	- 국가 단위, 도시 단위 
	- `그룹 풀` : 가상화 서버 풀, CPU 풀, 메모리 풀, 네트워크 풀... 등 **리소스 유형별로 모아 놓은 풀을 여러 개의 큰 풀로 묶음**
**`리소스 풀 모니터링`**
- 비용 계산
- 가용성 확인
#### 로드 밸런싱
**사용자의 요청을 여러 대의 서버로 분산시키는 법**
**`스케일링(Scaling)`** : 서버나 시스템의 용량과 성능을 확장/축소
- **확장**
	- `스케일-업(수직 스케일링)`
		- 확장 시, 서버 한 식를 계속 계속 해서 강화
	- `스케일-아웃(수평 스케일링)`
		- 확장 시, 서버를 여러 식을 가용하여 분산해서 강화
**로드 밸런싱**: 작업 부하를 분산 시켜 한 서버에 작업이 집중되지 않게 하는 기능, `로드밸런서(L4 스위치)`, `브로커 서버`

##### 목표: 이미지 관리(Blob storage 관리)
**==코드를 실행시켜서 Blob Storage에 파일 추가==**
0. 파이썬 스토리지 모듈 설치
```
# Windows cmd
pip install python-storage-blob
```
1. python 코드 작성
```
# Vscode - Upload
import os
from azure.storage.blob import BlobServiceClient

try:
  print("한국방송통신대학교 클라우드 컴퓨팅 Blob 파일 업로드")
  connect_str = "<연결 문자열>"
  blob_service_client = BlobServiceClient.from_connection_string(connect_str)
  container_name = "<컨테이너 이름>"

  local_file_name = "main_carousel.png" 

  container_client = blob_service_client.get_container_client(container=container_name)

  print("\nUploading to Azure Storage as blob:\n\t" + local_file_name)
  with open(file=os.path.join('', local_file_name), mode="rb") as data:
    blob_client = container_client.upload_blob(name=local_file_name, data=data, overwrite=True)
  
except Exception as ex: 
  print('Exception:') 
  print(ex)
```

```
# Vscode - Download
import os
from azure.storage.blob import BlobServiceClient

try:
  print("한국방송통신대학교 클라우드 컴퓨팅 Blob 파일 다운로드")
  connect_str = "<연결 문자열>"
  blob_service_client = BlobServiceClient.from_connection_string(connect_str)
  container_name = "<컨테이너 이름>"

  remote_file_name = "main_carousel.png" 
  local_file_name = "main_carousel_down.png"

  blob_client = blob_service_client.get_blob_client(container=container_name, blob=remote_file_name)

  print("\nDownloading blob from Azure Storage:\n\t" + remote_file_name)

  with open(file=os.path.join('', local_file_name), mode="wb") as download_blob:
        download_stream = blob_client.download_blob()
        download_blob.write(download_stream.readall())

except Exception as ex: 
  print('Exception:')
  print(ex)
```

```
#Vscode - Delete
import os
from azure.storage.blob import BlobServiceClient

try:
  print("한국방송통신대학교 4학년 2학기 클라우드 컴퓨팅")
  connect_str = "<연결 문자열>"
  blob_service_client = BlobServiceClient.from_connection_string(connect_str)
  container_name = "<컨테이터 이름>"

  remote_file_name = "main_carousel.png"

  blob_client = blob_service_client.get_blob_client(container=container_name, blob=remote_file_name)

  print("\nDeleting a blob from Azure Storage: \n\t" + remote_file_name)
  blob_client.delete_blob()

except Exception as ex: 
  print('Exception:') 
  print(ex)
```
`<컨테이너 이름>` : azure.스토리지계정.해당 스토리지 컨테이너 명
`<연결문자열>` : 보안 + 네트워킹 탭 > 액세스 키 탭 > 연결문자열 > copy&paste
2. 코드 실행
```
# cmd
# py 파일과 업로드 할 파일을 같은 경로에 위치
python <파일명>.py
```
3. 업로드 확인
#### Claude에게 질문 내용

>그러니까 정리하면 리소스는 IDC내에 있는 하나의 단일 서버에서 하이퍼바이저로 논리적으로 분할하여 자원을 할당받고,
> 나는 할당받은 자원(인스턴스)에서 Docker로 애플리케이션을 컨테이너화 하여 사용할 수 있다는거지?

>호스트 OS > 하이퍼바이저 OS 일 거고, Docker가 요청하는 내용은 하이퍼바이저 OS가 받아서 호스트 OS에게 전달하나?
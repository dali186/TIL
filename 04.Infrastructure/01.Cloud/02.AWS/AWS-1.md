### IAM(Identity and Access Management)
1. AWS 계정에 대한 공유 엑세스
2. 세분화된 권한 부여
3. Multi Factor 인증(MFA)
4. Identity Federation

### 사용자(Users), 그룹(Groups), 역할(Roles), 정책(Policy)
1. 사용자
	- 사용자는 자격증명(Credentials)을 갖는 최소 단위.
	- AWS를 사용하는 개인이나 서비스를 나타냄.
	- 각 사용자는 하나의 AWS 계정에서만 파생된다.
	- 각 사용자마다 권한정책을 적용할 수 있다.
2. 그룹
	- 사용자들을 논리적으로 묶은 단위.
	- 그룹 별로 정책을 지정할 수 있다.
		- 정책은 사용자 개별의 정책으로도 연결됨.
3. 정책
	- AWS에서 권한을 정의하는 JSON 문서.
	- 특정 리소스에 대한 액세스를 허용하거나 거부하는 규칙을 정의.
	```JSON
	{
		"Version": "2025-05-19",
		"Statement": [
			{
				"Effect": "Allow",
				"Action": ["s3:GetObject", "s3:PutObject"],
				"Resource": "arn:aws:s3:::example-bucket/*"
			}
		]
	}
	```
	- Effect
		- Allow(허용), Deny(거부) 두 개의 값만을 가짐.
		- 특정 작업을 허용할지 거부할지 결정.
	- Action
		- 수행할 작업을 정의.
	- Resource
		- 작업이 적용되는 특정 AWS 리소스를 지정.
		- ARN(Amazon Resource Name)을 사용하여 리소스 식별.
	- 권한
		- 서비스 엑세스 권한 수준을 구체적으로 지정.
4. 역할 (Roles)
	- 사람이 아닌 AWS 서비스, 외부 사용자, 다른 AWS 계정 등에게 권한을 위임하기 위한 임시 권한 부여 수단.
	- 역할 자체도 정책을 연결하여 권한을 정의하지만, IAM 사용자처럼 자격 증명을 가지지 않음.
	- 특정 주체가 역할을 AssumeRole(맡는 행위) 하여 권한을 일시 획득.
	- 예) EC2 인스턴스가 S3에 접근할 때 EC2에 역할을 부여하거나, 크로스 계정 접근 시 역할 사용.

**역할(Roles)에 대한 추가 이해**
역할 == 임시 보안 자격 증명(Temporary Security Credentials)
즉, 특정 사용자에게 정책을 부여했다가 회수하는 것과 동일한 의미.
보안성과 관리 편의성 측면에서 역할 + 임시 자격증명 방식을 사용한다.

## ✅ Launch Template 생성 가이드 (Nginx 포함)

### 1. EC2 > Launch Templates > [Create launch template] 클릭

- **Launch template name**: `nginx-template` (예시)
    
- **Template version description**: `v1`
    
- **AMI ID**: Ubuntu 22.04 (또는 원하는 Ubuntu AMI 선택)
    
- **Instance type**: `t2.micro` (프리티어 가능)
    
- **Key pair**: 원하는 키 페어 선택
    

---

### 2. **Network settings**

- **VPC**: 직접 만든 `my-vpc` 선택
    
- **Subnet**: `my-public-subnet` 선택
    
- **Auto-assign public IP**: **Enable**
    

---

### 3. **Security Group**

- 새로 생성 또는 기존 사용
    
    - Inbound rule:
        
        - SSH (TCP 22) — 내 IP
            
        - HTTP (TCP 80) — Anywhere (0.0.0.0/0)
            

---

### 4. **Advanced details → User data에 아래 스크립트 입력**

```bash
#!/bin/bash
sudo apt update -y
sudo apt install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx
```

> 이 스크립트는 인스턴스 부팅 시 자동으로 Nginx를 설치하고 시작해 줍니다.

---

### 5. 나머지 기본값 유지 → [Create launch template]

---

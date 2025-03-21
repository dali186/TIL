환경변수 등록하기
### 1. mongosh 설치 확인

- **MongoDB와 함께 설치된 경우**:  
    MongoDB를 설치하면 mongosh가 기본적으로 포함됩니다. 설치 경로는 보통 다음과 같습니다:
    
    text
    
    CollapseWrapCopy
    
    `C:\Program Files\MongoDB\Server\<version>\bin`
    
    예: C:\Program Files\MongoDB\Server\7.0\bin
- **별도로 설치한 경우**:  
    mongosh를 독립적으로 다운로드했다면, 압축을 푼 폴더 내 bin 디렉토리를 확인하세요(예: C:\mongosh\bin).

설치 경로를 모를 경우:

- 파일 탐색기에서 mongosh.exe를 검색해 위치를 찾으세요.

---

### 2. 환경 변수 Path에 경로 추가

Windows에서 CMD가 mongosh를 인식하려면, mongosh.exe가 있는 디렉토리를 Path에 추가해야 합니다.

#### 방법 1: GUI로 설정

1. **시스템 속성 열기**:
    - 키보드에서 Windows 키 + R → sysdm.cpl 입력 → Enter.
    - 또는 "제어판 → 시스템 → 고급 시스템 설정"으로 이동.
2. **환경 변수 편집**:
    - "고급" 탭에서 **"환경 변수"** 버튼 클릭.
3. **Path에 경로 추가**:
    - "사용자 변수" 또는 "시스템 변수"에서 Path 항목을 찾아 **"편집"** 클릭.
    - **"새로 추가"** 버튼을 눌러 mongosh 경로 입력:
        
        text
        
        CollapseWrapCopy
        
        `C:\Program Files\MongoDB\Server\7.0\bin`
        
        (실제 설치 경로로 변경하세요.)
    - "확인" 클릭.
4. **설정 저장**:
    - 모든 창에서 "확인"을 눌러 닫습니다.

#### 방법 2: CMD로 설정

CMD에서 명령어로 설정하려면:

1. CMD를 **관리자 권한**으로 실행:
    - "시작" → "cmd" 입력 → 우클릭 → "관리자 권한으로 실행".
2. 아래 명령어 입력:
    
    cmd
    
    CollapseWrapCopy
    
    `setx PATH "%PATH%;C:\Program Files\MongoDB\Server\7.0\bin" /M`
    
    - 경로는 실제 mongosh.exe가 있는 경로로 변경.
    - /M은 시스템 변수에 적용(관리자 권한 필요).
3. CMD 재시작:
    - 명령어가 적용되려면 기존 CMD 창을 닫고 새로 열어야 합니다.
## Lab 사전 준비사항 

### Container SL설정을 위한 사전 작업 
Microsoft Entra ID에서 Microsoft 365 그룹에 민감도 라벨 할당: Microsoft Entra 기능을 사용하여 민감도 라벨 지원을 활성화해야 합니다. 이를 통해 Microsoft 365 그룹에 민감도 라벨을 할당할 수 있으며, 이러한 라벨은 Microsoft Purview 포털에서 게시되고 그룹 및 사이트에 대해 구성됩니다

---

## Windows 

### Powershell 설치
   
```powershell
 winget search Microsoft.PowerShell

Name               Id                           Version Source
---------------------------------------------------------------
PowerShell         Microsoft.PowerShell         7.5.0.0 winget
PowerShell Preview Microsoft.PowerShell.Preview 7.6.0.2 winget
winget install --id Microsoft.PowerShell --source winget
```

### Microsoft Entra ID에서 Microsoft 365 그룹에 민감도 라벨 할당을 위한 사전작업

1. 관리자권한으로 PowerShell 프롬프트를 열고 cmdlet을 실행하는 데 필요한 그래프 모듈을 설치합니다.

```powershell
![image](https://github.com/user-attachments/assets/cb08c736-ab41-4663-87e3-86c4b4be8751)
```

2. 테넌트에 연결합니다. (별도 외부 페이지에서 인증 진행)
```powershell
Connect-MgGraph -Scopes "Directory.ReadWrite.All" 
```

3. Microsoft Entra 조직의 현재 그룹 설정을 가져오고 현재 그룹 설정을 표시합니다. 
```powershell
$grpUnifiedSetting = Get-MgBetaDirectorySetting | Where-Object { $_.Values.Name -eq "EnableMIPLabels" } $grpUnifiedSetting.Values
```

이 Microsoft Entra 조직에 대한 그룹 설정이 만들어지지 않은 경우 빈 화면이 표시됩니다. 이 경우 먼저 설정을 만들어야 합니다. Microsoft Entra cmdlet의 단계에 따라 그룹 설정 구성하여 이 Microsoft Entra 조직에 대한 그룹 설정을 만듭니다.

---

## MAC

1. Spotlight 검색 (Command + Space) → terminal 입력 → Enter
2. Homebrew 설치 확인

```bash
brew --version
```
* ✅ 버전이 출력되면 → Homebrew가 이미 설치된 상태
* ❌ ‘command not found’ 오류 → 아래 명령어로 Homebrew를 설치

3. Homebrew 설치
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

4. 설치확인
```bash
brew --version
```


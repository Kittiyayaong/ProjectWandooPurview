## Lab 사전 준비사항 

### 라벨 설정을 위한 사전 작업 
Microsoft Purview에서 Microsoft 365 Groups, Teams, SharePoint 사이트에 민감도 라벨(Sensitivity Label)을 적용하기 위해, Entra ID 테넌트에 EnableMIPLabels 설정을 활성화하는 작업을 수행합니다.

---

## ✅ Windows 

### * Powershell 설치
   
```powershell
 winget search Microsoft.PowerShell

Name               Id                           Version Source
---------------------------------------------------------------
PowerShell         Microsoft.PowerShell         7.5.0.0 winget
PowerShell Preview Microsoft.PowerShell.Preview 7.6.0.2 winget
winget install --id Microsoft.PowerShell --source winget
```

### * Microsoft Entra ID에서 Microsoft 365 그룹에 민감도 라벨 할당을 위한 사전작업

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

## ✅ MAC

### * macOS 환경 준비
1. Terminal 실행: Command + Space → terminal 입력 → Enter

2. Homebrew 설치 확인

```bash
brew --version
```
<img width="682" alt="스크린샷 2025-06-29 오전 7 15 23" src="https://github.com/user-attachments/assets/626dc0db-4757-41b3-a269-21da5fba6eed" />

* ✅ 버전이 출력되면 → Homebrew가 이미 설치된 상태
* ❌ ‘command not found’ 오류 → 아래 명령어로 Homebrew를 설치

3. Homebrew 설치
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
<img width="1440" alt="스크린샷 2025-06-29 오전 7 17 46" src="https://github.com/user-attachments/assets/e75d0977-2a0a-4b92-8d87-6abad6e56c3f" />

4. 설치확인
```bash
brew --version
```
<img width="464" alt="image" src="https://github.com/user-attachments/assets/dd53cda3-6eb9-4150-8088-c0fba2a0fffb" />

5. PowerShell 설치
```bash
brew install --cask powershell
```

6. Powershell 설치 완료 실행: 프롬프트가 PS > 로 바뀌면 성공적
```bash
pwsh
```
<img width="382" alt="image" src="https://github.com/user-attachments/assets/7c1a9253-9309-4563-ae34-3d61487f1b5f" />

### * Microsoft Graph 모듈 설치

1. PowerShell에서 Microsoft Graph 모듈 설치; PowerShell (pwsh) 진입 후 아래 명령어를 실행, 
```bash
Install-Module Microsoft.Graph -Scope CurrentUser
```

2. 설치 확인: 이미지와 같이 나오면, 정상 
```bash
Get-Module Microsoft.Graph -ListAvailable
```
<img width="675" alt="스크린샷 2025-06-29 오전 7 33 12" src="https://github.com/user-attachments/assets/8a6dca68-aada-41f0-9d38-36011cf1b911" />

###  Graph 테넌트 연결

1. 계정 연결
```bash
Connect-MgGraph -Scopes "Directory.ReadWrite.All"
```
<img width="685" alt="image" src="https://github.com/user-attachments/assets/ab4b29e2-9b5f-4c23-9354-3751a0adf492" />

### * Microsoft Graph Beta 모듈 설치

1. 베타 모듈 추가 설치: 설치 시 [Y]/[A] 선택지가 나오면 A + Enter 로 진행.
```bash
Install-Module Microsoft.Graph.Beta -Scope CurrentUser
```

> ⭐️ Beta 모듈 설치 여부를 확인하려면
> ```bash
> Get-Module Microsoft.Graph.Beta -ListAvailable
> ```

2. 설치 후, Beta 모듈 Import (진행 더딜시에 control+C로 중단 후 12번 진행) 
```bash
Import-Module Microsoft.Graph.Beta
```

### * EnableMIPLabels 설정 확인 및 적용

1. Microsoft Entra 조직(테넌트)에 EnableMIPLabels 설정이 되어 있는지 확인 (EnableMIPLabels = Microsoft 365 그룹과 SharePoint 사이트에 민감도 라벨(Sensitivity Label) 을 적용할 수 있도록 활성화하는 기능)
```bash
$grpUnifiedSetting = Get-MgBetaDirectorySetting | Where-Object { $_.Values.Name -eq "EnableMIPLabels" }
$grpUnifiedSetting.Values
```

2. EnableMIPLabels 설정 확인 및 적용: 아래 명령어를 PowerShell(Beta 모듈 Import된 상태)에서 실행합니다.
```powershell
$grpUnifiedSetting = Get-MgBetaDirectorySetting | Where-Object { $_.Values.Name -eq "EnableMIPLabels" }
$grpUnifiedSetting.Values
```
> 결과 해석
> * 값이 출력되면: 이미 설정 완료 (예: EnableMIPLabels True)
> * 값이 없거나 빈 결과면: 설정이 없는 상태 → 아래 단계로 생성 필요

3. EnableMIPLabels 설정 추가: 실행 후 새로운 설정 ID가 출력되면 정상적으로 적용
```powershell
$setting = @{
    DisplayName = "Group.Unified"
    TemplateId = (Get-MgBetaDirectorySettingTemplate | Where-Object {$_.DisplayName -eq "Group.Unified"}).Id
    Values = @(
        @{Name="EnableMIPLabels"; Value="True"}
    )
}
New-MgBetaDirectorySetting -BodyParameter $setting
```

4. 설정 적용 여부 최종 확인: 아래 명령어로 EnableMIPLabels 설정값이 True인지 확인
```powershell
$grpUnifiedSetting = Get-MgBetaDirectorySetting | Where-Object { $_.Values.Name -eq "EnableMIPLabels" }
$grpUnifiedSetting.Values
```
| Name            | Value |
| --------------- | ----- |
| EnableMIPLabels | True  |

<img width="808" alt="image" src="https://github.com/user-attachments/assets/9a0b240a-d2c4-421b-89f5-d29bb8ea13bc" />


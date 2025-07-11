# Purview Lab – Wandoo Sales Deal Protection & Insider Exfiltration Monitoring

## 시나리오 개요

Wandoo-Sales 그룹의 B2B Deal 관련 **영업 기밀 자료**를 보호하기 위한 Lab.

### **목표**

1. Sales Deal 라벨 ➔ 외부 공유 차단  
2. USB 저장, 클립보드 복사, 개인 클라우드 업로드 차단  

> Endpoint DLP와 Cloud DLP
> 
| 항목              | Cloud DLP                        | Endpoint DLP                        |
| --------------- | -------------------------------- | ----------------------------------- |
| **적용 위치**       | 클라우드 서비스 내 (클라우드 내에서 데이터 이동과 공유를 제어)                      | 사용자의 로컬 PC (디바이스 단에서 로컬 행위 제어)                          |
| **통제 가능 범위**    | 이메일, SharePoint, OneDrive, Teams | USB, 프린터, 클립보드, 로컬 앱, 개인 클라우드 업로드   |
| **Agent 필요 여부** | 불필요                              | 필요 (Intune MDM 관리 + MDE onboarding) |
| **주요 활용 예시**    | 외부 공유 차단, 암호화                    | USB 복사 차단, Slack 복사 차단              |


---

## ✅ 1. 사전 준비 (Pre-requisites)

### (1) 사용자 계정 생성

- **salesuser1**  
  - [Entra ID](entra.microsoft.com) > Users > + New user ➔ salesuser1 생성

### (2) 그룹 생성 – Wandoo-Sales

- Entra ID > Groups > + New group  
  ▸ Group type: Microsoft 365  
  ▸ Group name: Wandoo-Sales
  ▸ Members: salesuser1

### (3) Sensitivity Label – Confidential – Sales Deal

- Purview Portal > Information Protection > Labels > + Create a label
  - Name: Wandoo Confidential – Sales Deal
  - Scope: Files & Emails, Groups & Sites

> ⭐ Tips
>
> * Sales Deal 기밀 자료 (Files, Emails) 보호
> * Groups & Sites (Teams/SharePoint) 보호
> * USB, 클립보드, 개인 클라우드 업로드 차단
> * ➔ 회의(캘린더 이벤트) 데이터 보호는 본 시나리오 범위에 포함되지 않으므로 제외) 

  - Assgin permission: Wandoo-Sales / 권한은 **Editor**
    
> ⭐ Permission 정리
> 
| 옵션명                   | 권한 수준  | 설명                                                    |
| --------------------- | ------ | ----------------------------------------------------- |
| **Owner**             | 최고 권한  | - 모든 작업 가능<br> - 풀컨트롤 (Full control)                  |
| **Editor**            | 편집 권한  | - 보기(View)<br> - 편집(Edit)<br> - 저장(Save) 가능           |
| **Restricted Editor** | 제한 편집  | - 일부 편집만 허용<br> - 복사/추출, 저장 등 제한 가능                   |
| **Viewer**            | 보기 전용  | - 열람만 가능<br> - 편집, 복사, 추출 불가                          |
| **Custom**            | 사용자 정의 | - 세부 권한 직접 선택 가능<br> - 예: 복사허용, 추출허용 여부 등 세부 체크박스 활성화 |

  - Access content marking: “Wandoo Sales Confidential” 워터마크
  - Auto-labeling enable
    - 조건: Sensitive info types
      - Korea Resident Registration Number
      - Korea Passport Number
      - Credit Card Number
    - message: [자동 적용] 이 파일은 영업 기밀 정보가 포함되어 Sales Deal 보호 라벨이 적용되었습니다.
  - Group&Sites
    - Privacy and External user access: 이 옵션을 활성화하면 그룹/팀의 프라이버시 설정까지 강제 가능 (예: Private)
    - External Sharing and Conditional Access: SharePoint 사이트 외부 공유 차단 + CA 정책 강제 (필수)
  - Privacy: Private/ external 공유 금지   
    - External sharing: 
      - Organization에 있는 사람들만 접근 (외부 누구도 접근 불가 ➔ 기밀자료 보호)
      - Conditional Access: 비관리 디바이스에서 접근 차단
  - Publish to: Wandoo-Sales 그룹
  - Policy setting: Users must provide justification to remove/downgrade label

---

## ✅ 2. DLP Policy 생성

### **목적**

Sales Deal 라벨 파일 ➔ USB, 클립보드, 개인 클라우드, 외부 공유 차단 + override 기록

- Purview > Data Loss Prevention > Policies > + Create policy  
  ▸ Template: Custom policy  
  ▸ Name: Wandoo – Sales Deal Exfiltration Block  
  ▸ Locations:
    - OneDrive and SharePoint
    - Devices (Endpoint DLP)
  ▸ Users: Include ➔ Wandoo-Sales 그룹
  - **Conditions**
    - Content contains:
      - Sensitivity label: Wandoo Confidential – Sales Deal
  - **Actions** (개인 클라우드 업로드 관련 항목은 하기 Tips 참고)
    
| 행위 | Action 설정 | 효과 |
|--|--|--|
| 외부 공유 | Block | OneDrive/SharePoint ➔ 외부 공유 차단 + Policy Tip (“Sales Deal 자료는 외부 공유 불가. 문의: secops@contoso.com”) |
| USB 저장 | Block | Endpoint ➔ USB 저장 차단 + 사용자 알림 |
| 클립보드 복사 | Block | Endpoint ➔ 복사-붙여넣기 차단 (Slack, 메모앱 등) |
| 개인 클라우드 업로드 | Block | Endpoint ➔ 개인 OneDrive, Gmail, Dropbox 업로드 차단 |

---
> ⭐Tips. 개인 클라우드 업로드 
> <img width="931" alt="image" src="https://github.com/user-attachments/assets/154b6228-f4b5-4236-a367-672aa668ce50" />

> ⭐Tips. Global Block List
>
> <img width="696" alt="image" src="https://github.com/user-attachments/assets/2672aa18-c80c-4650-8fbf-3f0b3aacbf76" />
>
> * 설정 위치 : Purview > Setting > DLP > Browser and domain restrictions to sensitive data > Service domains
> * Service domain에 해당 도메인 Url 기입 후, 상단에 **Block**처리

> ⭐Tips. Sensitive service domain groups
>
> * 목적: 도메인 그룹을 만들어 ➔ 정책별로 다른 액션 지정하는데 사용
>
| 도메인 그룹             | 기본 Block | 선택적 다른 액션  |
| ------------------ | -------- | ---------- |
| `drive.google.com` | Block    | Audit only |
| `dropbox.com`      | Block    | Block      |





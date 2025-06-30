# Purview Lab – Wandoo Sales Deal Protection & Insider Exfiltration Monitoring

## 시나리오 개요

Wandoo-Sales 그룹의 B2B Deal 관련 **영업 기밀 자료**를 보호하기 위한 Lab.

### **목표**

1. Sales Deal 라벨 ➔ 외부 공유 차단  
2. USB 저장, 클립보드 복사, 개인 클라우드 업로드 차단  
3. Override with justification ➔ Insider Risk Trigger  
4. Teams 욕설/폭언 ➔ Communication Compliance Alert

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
  - Assgin permission: Wandoo-Sales / 권한은 **Editor**
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
| Override with justification | Allow override with justification | override 시 사유 기록 ➔ IRM Trigger 가능 |

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
| 도메인 그룹             | 기본 Block | 선택적 다른 액션  |
| ------------------ | -------- | ---------- |
| `drive.google.com` | Block    | Audit only |
| `dropbox.com`      | Block    | Block      |

---

## ✅ 3. Insider Risk Management Policy 생성

### **목적**

Override 기록, USB 저장 시도, 클라우드 업로드 시도 ➔ Trigger ➔ 사용자 모니터링

- Purview > Insider Risk Management > Policies > + Create policy  
  ▸ Template: Data leaks by risky users  
  ▸ Name: Wandoo – Sales Deal Insider Exfiltration Monitoring  
  ▸ Users & Groups: Wandoo-Sales 그룹  
  ▸ Priority content: Sensitivity label ➔ Wandoo Confidential – Sales Deal  
  ▸ Indicators: (금일 랩에서는 해당 indicator 활용이 불가하여 진행하지 않습니다.) 
    - Creating or copying files to USB 
    - Copy to personal cloud storage
    - Sending email with attachment externally
    - Override justification recorded
  ▸ Triggering events:
    - DLP policy match
    - Download from SharePoint or OneDrive

---

## ✅ 4. Communication Compliance Policy 생성

### **목적**

Teams 채팅 내 욕설/폭언 ➔ 탐지 ➔ Reviewer Alert

- Purview > Communication Compliance > Policies > + Create policy  
  ▸ Name: Wandoo – Sales Communication Monitoring  
  ▸ Users: salesuser1  
  ▸ Templates: Offensive language  
  ▸ Channels: Teams chat & Teams channel messages  
  ▸ Reviewers: security@contoso.com

---

## ✅ 5. 테스트 및 검증

### **[Case 1] 외부 공유 차단**

- salesuser1 ➔ OneDrive 파일 외부 공유 시도

✅ **기대 결과**: 공유 차단 + Policy Tip 표시

---

### **[Case 2] USB 저장 차단**

- salesuser1 ➔ 파일을 USB로 저장 시도

✅ **기대 결과**: 저장 차단 + 경고 알림

---

### **[Case 3] 클립보드 복사 차단**

- salesuser1 ➔ 파일 내용 복사 후 Slack 등 붙여넣기 시도

✅ **기대 결과**: 복사 차단

---

### **[Case 4] 개인 클라우드 업로드 차단**

- salesuser1 ➔ 개인 Gmail, Dropbox 업로드 시도

✅ **기대 결과**: 업로드 차단

---

### **[Case 5] Override 시도**

- salesuser1 ➔ Block 정책 override 시도 + 사유 입력

✅ **기대 결과**: override 성공 여부와 관계 없이 IRM Alert 생성

---

### **[Case 6] Teams 욕설 발송**

- salesuser1 ➔ Teams 채팅에서 욕설 발송

✅ **기대 결과**: Communication Compliance Alert 생성 ➔ Reviewer 알림

---

## ✅ 6. 결과 요약

| 기능 | 결과 |
|--|--|
| DLP policy | Sales Deal 라벨 파일 ➔ 외부 공유, USB 저장, 클립보드 복사, 개인 클라우드 업로드 차단 |
| Override with justification | override 시도 시 사유 기록 ➔ IRM Trigger |
| IRM policy | USB 저장, 클라우드 업로드, override 기록 ➔ Risk Alert 생성 |
| Communication Compliance | 욕설/폭언 ➔ Reviewer Alert |

---

## ✅ 7. 추가 Tips

- Auto-labeling: 영업 Deal 키워드 기반 자동 라벨링
- Adaptive Protection: Risk 기반 DLP Enforcement (E5 Compliance 필요)
- MCAS 세션 제어 연계: 다운로드 차단 or 암호화 (Advanced Lab 가능)
- Exception group: 정책 제외 그룹 생성 가능 (예: Wandoo Sales Exception)

---


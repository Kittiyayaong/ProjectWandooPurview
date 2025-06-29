# Purview Lab – Wandoo HR Group Confidential Info Protection (Single HR User Setup)

## 시나리오 개요
Wandoo-HR 그룹이 다루는 HR 기밀 정보(주민등록번호, 계좌정보 등)를 외부 공유/열람 시 차단하거나 제한하고, 내부 구성원만 접근 가능하도록 설정

> **목표**  
> Wandoo HR 그룹 소속 사용자(hruser1)가 **Confidential – HR Info 라벨**이 붙은 파일을  
> OneDrive / SharePoint에서 **외부로 공유 시도 시 차단**하고,  
> **IRM 정책 Trigger ➔ 사용자 행동 모니터링**을 시작한다.

---

## ✅ **1. 사전 준비 (Pre-requisites)**
### **(1) 사용자 계정**
   [Microsoft Entra admin center](https://entra.microsoft.com) > Users > All users > + New user 로 **hruser1** 생성

### **(2) 그룹 생성 – Wandoo HR 그룹**

1. [Microsoft Entra admin center](https://entra.microsoft.com) > Groups > All groups > + New group
2. **Group type:** Microsoft 365
3. **Group name:** `Wandoo-HR`
4. **Group description:** Wandoo HR test group
5. **Members:** hruser1 추가
6. **Create**

---

> ⭐️ **Notes**
> 
> - Entra ID에서 생성된 사용자/그룹은 **Microsoft 365 admin center와 실시간 동기화**됩니다.
> - 그룹 생성 시 **Group type을 Microsoft 365로 선택**해야 Teams, SharePoint, DLP policy 대상 그룹으로 사용 가능합니다.

---

### **(3) Sensitivity Label 생성**

✅ **Confidential – HR Info 라벨**

1. **Purview Portal > Information Protection > Labels > + Create a label**
2. **Name:** `Wandoo Confidential – HR Info`
3. **Scope:** Files & Emails, Groups & Sites
4. **Item**:
   * Control Access: `Wandoo-HR`
   * Access content marking: `Wandoo-HR` Watermark 추가 
6. **Auto-labeling:** Off (수동 테스트)
7. **Group & Sites (Wandoo HR confidential data 를 외부 공유 차단 + 비인가 디바이스에서 접근 차단하여 보호)
   1. Privacy and external user access:  `Private`– Only members can access
   2. External sharing and Conditional Access:  
      - Control external sharing from labeled SharePoint sites: `Only People in your Organizaiton`
        : 이 라벨이 적용된 SharePoint 사이트의 외부 공유 설정을 강제로 변경합니다. (기존 사이트의 외부 공유 정책을 무시하고 라벨 정책이 우선 적용됨)
      - Use Microsoft Entra Conditional Access to protect labeled SharePoint sites: `Block access`
        : Conditional Access 정책을 SharePoint site level로 강제 적용.(외부 공유 차단뿐만 아니라, 비인가 디바이스에서의 접근도 제한하여 보안을 강화해야 하는 경우)

> ⭐️ Block access 
>
> 설정은 보안 강도 최고 수준으로, HR 기밀정보를 관리되지 않는 개인 PC, BYOD 환경에서 접근하지 못하도록 차단함.

> ⚠️ 주의 사항
>
> 해당 설정은 SharePoint Admin Center > Access control > Unmanaged devices에서 Allow 또는 Limited access 대신 Block으로 설정되어 있어야 완전히 작동합니다.
>
> 또한 Entra Conditional Access 정책을 구성해야 실효성이 있습니다. (화면에 ‘There aren’t any authentication contexts configured’ 라는 메시지가 보임 → Authentication context를 먼저 생성 필요.)
 
8. **Publish Label**
   - **Policy Setting**: Users must provide a justification to remove a label or lower its classification ➔ Confidential – HR Info 라벨 제거/다운그레이드 시 사유를 남겨, IRM audit 및 DLP 조건 회피 방지.
   - **Policy Name:** `Wandoo Confidential HR Info Label Policy`
   - **Publish to:** `Wandoo-HR` 그룹
   - **Sites & Groups**: HR 전용 SharePoint 사이트 자동 라벨링 목적

> ⭐️ **Notes**
> “Confidential – HR Info 라벨을 파일에 적용 ➔ 외부 공유 차단 ➔ IRM Trigger”

> ⭐️ Groups & Sites scope가 필요한 경우
> 
> SharePoint 사이트 자체 또는 Teams 채널 전체를 Confidential 그룹/사이트로 분류하고
> 게스트 접근 제한, 외부 공유 차단, unmanaged device 차단 등의 컨테이너 단위 보호를 적용하려는 경우.
>
> 예시:
> 
> HR팀 SharePoint 사이트 전체에 Confidential 라벨 적용 ➔ 게스트 접근 자동 차단
> Teams HR 채널을 Confidential로 설정 ➔ 외부 사용자 초대 불가

---

## ✅ **2. DLP Policy 생성**

### **목적:** HR Info 라벨 파일 외부 공유 차단 ➔ IRM Trigger

1. **Purview > Data Loss Prevention > Policies > + Create policy**
2. **Template:** Custom policy
3. **Name:** `Wandoo – HR Confidential External Share Block`
4. **Locations:** OneDrive and SharePoint
5. **Users:** Include ➔ `Wandoo-HR` 그룹
6. **Conditions:**
   - Content contains ➔ **Sensitivity label: Confidential – HR Info**
7. **Actions:**
   - Block external sharing
   - User notification: On
   - Admin alert: On (보안팀 이메일 추가 가능)
8. **Review & Create**

---

## ✅ **3. IRM Policy 생성 (DLP Trigger 기반)**

### 🔹 **목적:** HR Info 외부 공유 시도 ➔ IRM Trigger ➔ User monitoring 시작

1. **Purview > Insider Risk Management > Policies > + Create policy**
2. **Template:** Data leaks by risky users
3. **Name:** `Wandoo – HR Confidential Data Leak Monitoring`
4. **Users:** `Wandoo-HR` 그룹
5. **Priority content:**
   - Sensitivity label ➔ `Confidential – HR Info`
6. **Indicators:**
   - Download from SharePoint or OneDrive
   - Sending email with attachments externally
7. **Scoring:** Get alerts for all activity
8. **Triggering events:**
   - ✅ Data loss prevention (DLP) policy match
9. **Review & Create**

---

## ✅ **4. 테스트 및 검증**

### **[Case 1] DLP 정책 검증**

1. **hruser1 계정으로 로그인**
2. OneDrive에서 새 파일 업로드 ➔ 수동으로 **Confidential – HR Info 라벨** 적용
3. **공유 버튼 클릭 ➔ externaltest@gmail.com** 외부 계정에 공유 시도

✅ **기대 결과**
- 파일 공유 차단됨
- 사용자에게 **Policy Tip 알림** 표시 ("외부 공유가 정책에 의해 차단되었습니다.")
- Purview > DLP Alerts 에서 alert 생성 확인

---

### **[Case 2] IRM Trigger 검증**

1. **위 Case 1 공유 차단 시도 후**, 관리자로 Purview Portal 접속
2. **Insider Risk Management > Alerts** 확인

✅ **기대 결과**
- hruser1 에 대한 new Alert 생성
- Alert 상세 내용에 **Trigger: DLP policy match** 표시
- Risk score 부여된 Event 기록 확인

---

## 결과 

| 기능 | 결과 |
|---|---|
| **DLP policy** | HR Info 라벨 파일 외부 공유 차단 + 사용자 알림 |
| **IRM policy** | DLP match 시 Trigger ➔ User risk monitoring 시작 ➔ Risk alert 생성 |

---

## **6. 추가 Tips**

- ✅ **Exception group**: 정책 제외 그룹 생성 가능 (예: Wandoo Security Exception)
- ✅ **Priority content**: Sensitivity label 설정으로 탐지 범위 강화
- ✅ **Communication Compliance 연계:** HR 그룹 Teams 채팅 욕설/차별 탐지 정책 추가 가능
- ❌ **HR connector trigger**: 현재 E5 (no Teams) 라이선스에서는 사용 불가
- ❌ **Adaptive Protection**: E5 Compliance 라이선스 필요



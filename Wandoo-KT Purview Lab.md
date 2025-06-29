# Wandoo-KT를 위한 purview 셀프 랩 시나리오 

## Purview Lab – Wandoo HR Group Confidential Info Protection (Single HR User Setup)

## 시나리오 개요

> **목표**  
> Wandoo HR 그룹 소속 사용자(hruser1)가 **Confidential – HR Info 라벨**이 붙은 파일을  
> OneDrive / SharePoint에서 **외부로 공유 시도 시 차단**하고,  
> **IRM 정책 Trigger ➔ 사용자 행동 모니터링**을 시작한다.

---

## ✅ **1. 사전 준비 (Pre-requisites)**

### **(1) 사용자 계정**

| 역할 | 계정 예시 | 설명 |
|---|---|---|
| **관리자** | admin@tenant.onmicrosoft.com | Global + Compliance Admin 권한 |
| **HR 사용자** | hruser1@tenant.onmicrosoft.com | Wandoo HR 담당자 |
| **외부 테스트 계정** | externaltest@gmail.com | 외부 공유 차단 테스트 |

**실습을 위해:**
- Microsoft 365 admin center > Users > Active users > + Add user 로 **hruser1** 생성

---

### **(2) 그룹 생성 – Wandoo HR 그룹**

1. Microsoft 365 admin center > Groups > Active groups > + Add a group
2. **Type:** Microsoft 365
3. **Name:** `Wandoo-HR`
4. **Description:** Wandoo HR test group
5. **Members:** hruser1 추가
6. **Finish**

---

### **(3) Sensitivity Label 생성**

✅ **Confidential – HR Info 라벨**

1. **Purview Portal > Information Protection > Labels > + Create a label**
2. **Name:** `Confidential – HR Info`
3. **Scope:** Files & Emails
4. **Encryption:** Optional (테스트 목적 Off 가능)
5. **Auto-labeling:** Off (수동 테스트)
6. **Publish Label**
   - **Policy Name:** `Confidential HR Info Label Policy`
   - **Publish to:** `Wandoo-HR` 그룹

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



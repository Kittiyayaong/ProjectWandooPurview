# Wandoo-KT를 위한 purview 셀프 랩 시나리오 

# Purview Lab – Sensitivity Label + IRM + DLP Policy

## 🎯 시나리오

“Confidential 라벨이 적용된 문서를 OneDrive 또는 SharePoint에서 다운로드 시 Risk alert 생성 ➔ DLP 정책으로 외부 공유 차단”

---

## ✅ 목적

1. **IRM 정책**: Confidential 라벨 파일 다운로드 탐지 ➔ Risk Alert 생성  
2. **DLP 정책**: Confidential 파일의 외부 공유 차단

---

### #### [Step 0] 사전 준비

- Microsoft Purview Portal 접속: [compliance.microsoft.com](https://compliance.microsoft.com)
- 테스트 사용자 계정 준비
- Confidential Sensitivity Label 미리 없으면 아래 Step 1에서 생성

---

### #### [Step 1] Sensitivity Label 생성

1. **Information Protection > Labels > + Create a label**
2. **Name:** `Confidential - Lab`
3. **Scope:** Files & Emails
4. **Encryption:** Optional (테스트 목적 Off 가능)
5. **Auto-labeling:** Disable (수동 테스트용)
6. **Publish Label**
   - **Policy Name:** `Confidential Label Policy`
   - **Publish to:** Test users

---

### #### [Step 2] DLP Policy 생성 (외부 공유 차단)

1. **Data Loss Prevention > Policies > + Create policy**
2. **Template:** Custom policy
3. **Name:** `Confidential File External Share Block`
4. **Locations:** OneDrive and SharePoint
5. **Conditions:**
   - Content contains ➔ **Sensitivity label: Confidential - Lab**
6. **Actions:**
   - **Block external sharing**
   - User notification: Enabled
   - Admin alert: Enabled
7. **Review & Create**

---

### #### [Step 3] IRM Policy 생성 (다운로드 Risk alert)

1. **Insider Risk Management > Policies > + Create policy**
2. **Template:** Data leaks by risky users
3. **Name:** `Confidential Download Risk Alert`
4. **Users:** All test users
5. **Priority content:**
   - Sensitivity label ➔ **Confidential - Lab**
6. **Indicators:**
   - Download from SharePoint or OneDrive
7. **Scoring:** Get alerts for all activity
8. **Review & Create**

---

### #### [Step 4] 테스트

1. 테스트 사용자 계정으로 **Confidential - Lab 라벨 적용 파일** OneDrive 업로드
2. 같은 계정으로 파일 다운로드 ➔ **IRM Alert 생성** 확인
3. 다른 외부 계정으로 파일 공유 시도 ➔ **DLP 정책으로 차단** 확인

---

## 결과 

| 기능 | 결과 |
|---|---|
| **IRM Policy** | 다운로드 탐지 ➔ Risk Alert |
| **DLP Policy** | 외부 공유 차단 + 사용자 알림 |

---

### Tips

- **Adaptive Protection:** E5 Compliance 필요 (현재 라이선스에서는 미지원)
- **Communication Compliance:** 욕설, 혐오 표현 탐지 정책 추가 가능
- **확장:** Auto-labeling 정책과 연계하여 완전 자동화 시나리오 구축 가능


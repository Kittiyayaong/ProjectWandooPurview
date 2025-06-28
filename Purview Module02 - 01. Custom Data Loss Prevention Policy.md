# Purview Module 02. Data Loss Prevention

## Lab 1. Custom Data Loss Prevention Policy

AI 활용 데이터 유출 방지 시나리오 & Purview Custom DLP Policy 설정

## 1. 시나리오 개요

최근 조직 내 사용자들이 ChatGPT, Copilot, Copilot for Security 등 **AI 기반 서비스**를 활용하면서  
고객 개인정보, 기밀 문서, 소스코드 등 민감 데이터를 AI Prompt에 복사해 붙여넣는 사례가 급증.

* 리스크: AI 서비스는 입력 데이터를 학습 및 로그로 저장할 수 있어 **데이터 유출 위험** 존재
  * 고객명단(이메일 포함)을 복사해 AI에 요약 요청
  * 소스코드를 복사해 AI에 코드 리뷰 요청

---

## ✅ 2. 방지 시나리오

| 시나리오 | 설명 |
|---|---|
| **Prompt에 개인정보 포함** | 고객 이메일, 전화번호, 주민등록번호 등 |
| **Prompt에 기밀 코드 포함** | 소스코드, API Key, 내부 알고리즘 |
| **Prompt에 경영 기밀 포함** | 재무 데이터, M&A 계획, 전략 문서 |

Microsoft Purview DLP의 **Custom Policy**를 통해 방지 
* **AI 서비스 접속 시 데이터 업로드/복사 방지**
* **조건 매칭 시 사용자 알림 + 차단** 조치

---

## 3. Custom DLP Policy 설정 방법

### ✨ [Step 1] 정책 생성

1. Microsoft Purview > **Data Loss Prevention** > Policies > **Create policy**
2. **Custom policy** 선택

---

### ✨ [Step 2] Scope 선택

- **Data in browser activity**
  - AI SaaS 앱에 붙여넣는 데이터를 보호 (Defender for Cloud Apps 필요)

또는

- **Data stored in connected sources**
  - Copilot for Microsoft 365 Prompt 내 입력값도 M365 서비스 내 보호 가능

---

### ✨ [Step 3] Locations 지정

- **Cloud apps** (Defender for Cloud Apps 연결 필요)
  - ChatGPT, Bard, Copilot for Security 등 사용 중인 AI 서비스 URL 포함
- **Devices** (Endpoint DLP 연계 시)
  - 디바이스 전반의 Clipboard, App access 제어 가능

---

### ✨ [Step 4] Policy rule 설정

#### ✅ Conditions

- **Content contains:**
  - Sensitive info types
    - Korea Resident Registration Number (주민등록번호)
    - Korea Passport Number (여권번호)
    - Credit Card Number (신용카드번호)
    - [조직 내 정의된 Custom Info Types] (예: Project Code Pattern)

또는

- **Content contains labels:**
  - 이미 Microsoft Purview Information Protection에서 민감도 라벨을 적용 중인 경우

---

#### ✅ Actions

- **User notification:**
  - 팝업 또는 메일로 경고 (예: “조직 정책에 의해 해당 데이터 전송이 제한됩니다.”)

- **Block:**
  - 조건 매칭 시 전송 차단

- **Audit:**
  - 관리자가 시도 내역을 검토할 수 있도록 로깅

---

### ✨ [Step 5] User overrides 설정

- (선택) 사용자가 정당한 사유가 있으면 Justification 후 override 가능 설정

---

### ✨ [Step 6] Policy mode

- **Test with notifications**
  - 정책 영향 범위를 우선 테스트
- **Enforce**
  - 충분히 검증 후 실제 차단/경고 적용

---

## ✅ 4. 최종 요약

| 목표 | 설정 요약 |
|---|---|
| **AI Prompt에 민감정보 유출 방지** | Purview DLP Custom Policy 생성 → Sensitive Info Types 조건 추가 → Locations에 AI 서비스 포함 → Action에서 Block/Notify 설정 |

---

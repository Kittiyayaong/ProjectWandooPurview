# Purview Module 02. Data Loss Prevention

## Lab 2. Custom Data Loss Prevention Policy

시나리오 
1. **Microsoft Teams Prompt & 채팅 데이터 보호**
2. **Microsoft Copilot for M365 Prompt 보호**
3. **ChatGPT (외부 AI) Prompt 보호**

---

## 1️⃣ Microsoft Teams Prompt & Chat Protection

### 적용 시나리오

- Teams 채팅, 채널 메시지에 **고객 개인정보, 기밀 데이터, 소스코드** 입력/공유 방지
- 내부 협업 중 **불필요한 민감정보 노출 차단**

### 정책 구성 방법

#### [Step 1] 정책 생성

1. Microsoft Purview > **Data Loss Prevention** > Policies > **Create policy**
2. Data stored in connected sources: Copilot for Microsoft 365 Prompt 내 입력값도 M365 서비스 내 보호 가능

<img width="1414" alt="image" src="https://github.com/user-attachments/assets/9af9240d-80c1-4a80-be48-aa390646f312" />

3. **Custom policy** 선택

<img width="1419" alt="image" src="https://github.com/user-attachments/assets/01b9db6b-139d-4f9f-8160-36c503edf542" />

#### [Step 2] Name/ Admin/ Locations 지정

1. Name: Wandoo - Teams Prompt Data Protection
2. Admin: Full directory(Default) 유지
   
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/39290057-52f4-438e-ace0-dcc2c1d9405b" />

3. **Teams chat and channel messages*** 설정

<img width="1421" alt="image" src="https://github.com/user-attachments/assets/4d676c3e-af6b-4e8c-9ca3-06064ba32b2b" />

#### [Step 3] Policy rule 설정

<img width="1391" alt="스크린샷 2025-06-29 오전 8 30 52" src="https://github.com/user-attachments/assets/bcb16b76-c989-46e3-82f8-01840eacaadf" />

- **Condition**
  - Content contains: Sensitive info types (예: 주민등록번호, 여권번호, 신용카드번호 등)
  - Add condition → Content contains  → Sensitive info types 선택
    * 주민등록번호 (Korea Resident Registration Number)
    * 여권번호 (Korea Passport Number)
    * 신용카드번호 (Credit Card Number)

<img width="976" alt="스크린샷 2025-06-29 오전 8 34 28" src="https://github.com/user-attachments/assets/a3eac2d4-cba0-47fe-9080-bb65102c4f76" />

- **Actions**
  - Block everyone 선택: 내부 사용자 간에도 민감정보 공유를 방지하려는 목적으로 Shadow IT 또는 부주의로 인한 유출 리스크 최소화
   - Teams 채팅/채널 메시지에 정책 조건(Sensitive info types) 매칭 시:
     * 메시지 전송 차단
     * SharePoint, OneDrive, Teams 파일 접근 차단(해당 정책 Location 범위 내에서)

<img width="964" alt="스크린샷 2025-06-29 오전 8 35 46" src="https://github.com/user-attachments/assets/c6b07e7e-d033-4002-b7a1-d3059933eb9f" />
       
| 옵션                                              | 의미                             |
| ----------------------------------------------- | ------------------------------ |
| **Block everyone (기본 선택)**                      | 조직 내부/외부 모든 사용자에게 차단 적용        |
| **Block only people outside your organization** | 조직 외부 사용자(예: 고객, 파트너)에게만 차단 적용 |

- User notifications(Policy Tip/정책 차단 이유 사용자에게 표시): DLP 정책 조건 매칭 시, 사용자에게 알림(Prompt)을 표시하는 기능으로, Purview UI 상에서는 “User notifications”라고 표기되지만, Teams, Outlook 등 사용자 화면에는 Policy Tip 형태로 나타납니다.
   - Policy tip text: 🚫 Wandoo Security: 이 메시지는 주민등록번호, 여권번호, 카드번호 등 민감정보 포함으로 차단되었습니다. 안전한 공유를 위해 IT 보안팀과 상의해주세요. 

<img width="983" alt="image" src="https://github.com/user-attachments/assets/4641abf1-556f-48cb-8bba-be542d843711" />
 

- 그 외 설정

| 항목                     | 권장 설정                                                                                   |
| ---------------------- | --------------------------------------------------------------------------------------- |
| **User overrides**     | Off (Override 허용하지 않음)                                                                  |
| **Incident reports**   | Severity level = High<br>Send alert to admins = On<br>Add security team email if needed |

<img width="969" alt="스크린샷 2025-06-29 오전 8 41 36" src="https://github.com/user-attachments/assets/844f13e3-c7ac-47a9-96f0-49f7380510cc" />


#### [Step 4] Policy mode
- Run in simulation mode + Show policy tips로 설정 

| ✅ **옵션**                                         | **의미**                                                                          | **활용 시점**                                        |
| ------------------------------------------------ | ------------------------------------------------------------------------------- | ------------------------------------------------ |
| **1. Run the policy in simulation mode**         | 정책을 테스트 모드로 실행하여, 조건에 매칭되는 항목만 모니터링하고 실제 차단/조치는 하지 않음                           | - 정책 조건과 Scope 검증<br>- 조직 영향 없이 Rule match 상황 파악 |
| 🔹 **Show policy tips while in simulation mode** | Simulation mode 상태에서도 사용자에게 Policy Tip(알림) 표시 <br> **효과:** 사용자 인지 가능, 실제 차단은 없음 | - 사용자 교육 및 사전 안내 목적                              |
| **2. Turn the policy on immediately**            | 정책을 즉시 활성화(Enforce)하여, 조건에 매칭되는 항목을 차단/조치                                       | - 테스트 완료 후, 실제 보호 적용 시                           |
| **3. Leave the policy turned off**               | 정책을 비활성화 상태로 둠 (저장만)                                                            | - 아직 정책을 적용할 준비가 안된 경우                           |

---

## 2️⃣ Microsoft Copilot for M365 Prompt 보호

### 적용 시나리오

- **Microsoft Copilot for M365**에 **고객 개인정보, 기밀 데이터, 소스코드** 입력 방지
- Copilot Prompt에 민감정보가 그대로 입력되는 것을 차단하여, AI 처리로 인한 데이터 유출 리스크 최소화

---

### 정책 구성 방법

#### [Step 1] 정책 생성

1. Microsoft Purview > **Data Loss Prevention** > Policies > **Create policy**
2. **Data stored in connected sources** 선택  
   (Copilot Prompt도 Microsoft 365 서비스 내 데이터로 분류되어 보호 가능)
3. Custom policy로 선택

#### [Step 2] Name/ Admin/ Locations 지정
1. Name: **Wandoo - Copilot M365 Prompt Data Protection**
2. Admin: Full directory(Default) 유지
3. Location: Microsoft 365 Copilot (preview)

#### [Step 3] Policy rule 설정

 **Condition**
  - Content contains: Sensitive info types
  - Add condition → Content contains → Sensitive info types 선택
    * 주민등록번호 (Korea Resident Registration Number)
    * 여권번호 (Korea Passport Number)
    * 신용카드번호 (Credit Card Number)
      
- **Actions**
  - 차단 설정 불가 (Copilot Prompt 입력 차단은 정책 시뮬레이션 + 정책 팁 알림만 가능)
  - Copilot Prompt 내 정책 팁(Policy Tip) 표시를 통해 사용자에게 알림

- **User notifications (Policy Tip/정책 차단 이유 사용자에게 표시)**  
  DLP 정책 조건 매칭 시, 사용자에게 알림(Prompt)을 표시하는 기능.  
  Purview UI 상에서는 **“User notifications”**로 표기되며, Copilot Prompt에 Policy Tip 형태로 나타남.
  - Policy tip text:
    ```
    🚫 Wandoo Security: Copilot Prompt에 민감정보(주민등록번호, 여권번호, 카드번호 등) 입력이 탐지되었습니다. AI 처리 전 반드시 제거하세요.
    ```

#### [Step 4] Policy mode
- Run in simulation mode + Show policy tips로 설정 

| ✅ **옵션**                                         | **의미**                                                                          | **활용 시점**                                        |
| ------------------------------------------------ | ------------------------------------------------------------------------------- | ------------------------------------------------ |
| **1. Run the policy in simulation mode**         | 정책을 테스트 모드로 실행하여, 조건에 매칭되는 항목만 모니터링하고 실제 차단/조치는 하지 않음                           | - 정책 조건과 Scope 검증<br>- 조직 영향 없이 Rule match 상황 파악 |
| 🔹 **Show policy tips while in simulation mode** | Simulation mode 상태에서도 사용자에게 Policy Tip(알림) 표시 <br> **효과:** 사용자 인지 가능, 실제 차단은 없음 | - 사용자 교육 및 사전 안내 목적                              |
| **2. Turn the policy on immediately**            | 정책을 즉시 활성화(Enforce)하여, 조건에 매칭되는 항목을 차단/조치                                       | - 테스트 완료 후, 실제 보호 적용 시                           |
| **3. Leave the policy turned off**               | 정책을 비활성화 상태로 둠 (저장만)                                                            | - 아직 정책을 적용할 준비가 안된 경우                           |


- 그 외 설정

| 항목                     | 권장 설정                                                                                   |
| ---------------------- | --------------------------------------------------------------------------------------- |
| **User overrides**     | Off (Override 허용하지 않음)                                                                  |
| **Incident reports**   | Severity level = High<br>Send alert to admins = On<br>Add security team email if needed |

---

## 3️⃣ ChatGPT (외부 AI) Prompt 보호

### 적용 시나리오

- ChatGPT, Bard, Claude 등 **외부 AI 서비스 Prompt에 고객 개인정보, 기밀 데이터, 소스코드** 입력 방지
- Shadow IT 형태의 외부 AI 서비스 사용으로 인한 **데이터 무단 전송 리스크 차단**

### 정책 구성 방법

#### [Step 1] 정책 생성

1. Microsoft Purview > **Data Loss Prevention** > Policies > **Create policy**
2. **Data in browser activity** 선택  
   (Microsoft Defender for Cloud Apps + Edge 통합을 통해 브라우저 기반 SaaS 활동 보호)
3. **Custom policy** 선택


#### [Step 2] Name/ Admin/ Locations 지정

1. Name: **Wandoo - ChatGPT Prompt Data Protection**
2. Admin: Full directory(Default) 유지

![image](https://github.com/user-attachments/assets/39290057-52f4-438e-ace0-dcc2c1d9405b)

3. Location: **OpenAI ChatGPT**  
   (Defender for Cloud Apps Integration 필요)

<img width="1409" alt="스크린샷 2025-06-29 오전 9 09 32" src="https://github.com/user-attachments/assets/ca0449ac-2b6e-4643-9a59-1f1a3ffc9897" />


> ⭐️ Tips. ‘Data in browser activity’ 기반 DLP 정책은 **Microsoft Defender for Cloud Apps + Microsoft Edge 통합 기능**을 활용합니다.
> 
> | **브라우저** | **지원 여부** | **비고** |
> | ------------ | ------------ | -------- |
> | **Edge**    | ✅ 지원 | DLP 정책 작동 (Data in browser activity) |
> | **Chrome**  | ❌ 미지원 | 정책 적용 불가 |
> | **Safari**  | ❌ 미지원 | 정책 적용 불가 |
> | **Firefox** | ❌ 미지원 | 정책 적용 불가 |

> 권장 대응
>
> - **Microsoft Edge 사용 강제**: 조직 정책으로 AI Prompt 접근 시 Microsoft Edge 사용을 강제
> - **Endpoint DLP 구성**: Chrome 등 타 브라우저에서도 DLP가 필요하면 ➔ **Endpoint DLP(Device-based 정책)** 별도 구성 필요

#### [Step 3] Policy rule 설정

- **Condition**
  - Content contains: Sensitive info types
  - Add condition → Content contains → Sensitive info types 선택
    * 주민등록번호 (Korea Resident Registration Number)
    * 여권번호 (Korea Passport Number)
    * 신용카드번호 (Credit Card Number)

- **Actions** : text > Block으로 설정

<img width="1552" alt="스크린샷 2025-06-29 오전 9 17 22" src="https://github.com/user-attachments/assets/61623b68-3c27-40c6-9c26-d71e3c920477" />
  
| 옵션 | 의미 | 비고 |
| --- | --- | --- |
| **Text upload** | 사용자가 클라우드 앱(ex. ChatGPT, Gemini 등)에 **텍스트를 입력/업로드(프롬프트 포함)** 하는 행위 | Prompt 데이터 유출 차단 시 사용 |
| **File upload** | 파일 업로드 차단 | 비활성화 (선택 안됨) |
| **File download** | 파일 다운로드 차단 | 비활성화 (선택 안됨) |
| **Cut or copy data** | 잘라내기/복사하기 차단 | 비활성화 (선택 안됨) |
| **Paste clipboard data** | 붙여넣기 차단 | 비활성화 (선택 안됨) |


> ⭐️ Tips. **Policy Tip 설정**
> - 현재 **Data in browser activity (브라우저 기반 DLP)** 정책에는
>  - Outlook, Teams, SharePoint와 같은 M365 workload DLP와 달리
>  - **User notification (Policy Tip)** 설정 옵션이 존재하지 않음.

✔️ 즉,
- Audit Only: 사용자에게 별도 알림 없이 **관리자 로그만 기록**
- Block: 차단되지만, 차단 안내 메시지가 Edge 팝업으로 나타날 수 있으나 **Policy Tip으로 표시되지 않음**

- 그 외 설정

| 항목                     | 권장 설정                                                                                   |
| ---------------------- | --------------------------------------------------------------------------------------- |
| **User overrides**     | Off (Override 허용하지 않음)                                                                  |
| **Incident reports**   | Severity level = High<br>Send alert to admins = On<br>Add security team email if needed |


#### [Step 4] Policy mode
| 설정                                                                                                | 효과                                                                              |
| ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| **Run the policy in simulation mode + Turn the policy on if it’s not edited within fifteen days** | - 정책을 우선 시뮬레이션 모드로 실행<br>- 15일간 수정이 없으면 자동 Enforce<br>- 초기 테스트 + 자동 적용 시나리오에 적합 |


> ⭐️ TipsShow policy tips while in simulation mode: 현재 비활성화됨 (체크 불가)
> ➔ Data in browser activity 정책의 경우, Policy Tip 기능을 지원하지 않음
> (M365 내부 서비스에서는 표시 가능하지만, 브라우저 activity DLP에는 표시 불가)

---

> ⭐️ Tips. Data in browser activity 정책은 **Microsoft Edge + Defender for Cloud Apps Integration** 환경에서만 작동합니다. Chrome, Safari, Firefox에는 적용되지 않으므로, Endpoint DLP와 함께 병행 적용 권장.
>
> 1. **Data in browser activity 정책의 구조**
>   - Purview DLP의 이 기능은 **Microsoft Defender for Cloud Apps** 의 **session control (Conditional Access App Control)** 기능과 통합되어 동작.
>   - 즉, MDCA가 중간 proxy 역할을 하여 브라우저 활동을 모니터링 및 제어.
>
> 2. **작동 조건**
>   | 조건 | 필요 여부 | 비고 |
>   | --- | --- | --- |
>   | Microsoft Edge | ✅ 필수 | MDCA + Edge 통합 필요 |
>   | MDCA 라이선스 | ✅ 필수 | Microsoft 365 E5 / Microsoft Defender for Cloud Apps |
>   | Endpoint DLP | ❌ 선택 | 브라우저 기반 외 로컬 데이터 보호 용도로 병행 권장 |

### 🔗 [다음 Lab으로 이동하기 »](https://github.com/Kittiyayaong/ProjectWandooPurview/blob/main/Purview%20Module03%20-%2001.%20Insider%20Risk%20Management%20(IRM).md)

# Purview Module 02. Data Loss Prevention

## Lab 1. Custom Data Loss Prevention Policy

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

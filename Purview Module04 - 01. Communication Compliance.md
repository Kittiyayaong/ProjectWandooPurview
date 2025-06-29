<img width="1552" alt="image" src="https://github.com/user-attachments/assets/2eed536f-3d31-46d9-896d-140e5876c90d" /># Purview Module 04 - Other Purview Features

## Lab 1. Communication Compliance

### 시나리오 
- 최근 **Wandoo 조직**에서 고객 대응 메일과 Teams 채팅 내 **부적절한 표현(욕설, 성차별 발언 등)** 사용 사례 증가
- Compliance 팀 목표:
  - **Wandoo-Sales 그룹** 대상
  - **욕설, 차별, 폭력적 표현** 탐지
  - 탐지 시 **Risk alert 생성 ➔ Insider Risk Policy Trigger**
  - 반복 위반자는 **Adaptive Protection**으로 External communication 차단 예정
 
### Lab 목표

1. Communication Compliance Policy 생성
2. 욕설/차별 발언 탐지 조건 설정
3. Reviewer 지정 ➔ 검토 및 시정 요청 흐름 확인
4. **Insider Risk Management** Trigger로 연계

#### [Step 1] Microsoft Purview communication compliance policy 설정

1. Purview console > Solutions > **Communication Compliance**> **Policies > + Create policy** > Detect inappropriate content로 생성 

<img width="1335" alt="image" src="https://github.com/user-attachments/assets/7c3ea1f4-8dd4-47c4-ab80-9e26962e5303" />

* Name: Wandoo – Offensive Language Monitoring
* Users: **Wandoo-Sales**
* Reviewers: Compliance team (예: MOD Admin)

모두 설정 이후 **Customize policy** 클릭 

<img width="1552" alt="스크린샷 2025-06-29 오전 11 05 59" src="https://github.com/user-attachments/assets/a610bf55-5ca2-49a9-823b-8dfdf08055e6" />

#### [Step 2] Custom 세부 정보 

* Preserve policy matches: Communication Compliance 정책에서 탐지된 메시지(Policy match) 를 얼마나 오래 보존할지 결정하는 옵션입니다.

<img width="1552" alt="스크린샷 2025-06-29 오전 11 07 43" src="https://github.com/user-attachments/assets/1e38bbd5-817a-4556-bd15-e7f540e1c192" />

| 옵션                                        | 의미                                           |
| ----------------------------------------- | -------------------------------------------- |
| **Global Setting**                        | 조직의 Communication Compliance 기본 보존 기간을 따름    |
| **1 month / 6 months / 1 year / 7 years** | 탐지된 메시지(예: 욕설 포함 Teams 채팅) 를 별도로 지정한 기간만큼 보존 |

* locations: Teams & Viva Engage
  
#### [Step 3] conditions
기본적으로 욕설 탐지 classifier가 포함되므로, 추가 필터링 조건 없이도 탐지 가능하나, 필요 시 아래 조건을 추가해 탐지 범위를 좁힐 수 있습니다.

| 조건 옵션                                         | 설명                               | 권장 여부                  |
| --------------------------------------------- | -------------------------------- | ---------------------- |
| **Trainable classifiers**                     | 욕설, 차별, 위협 발언 등 탐지 classifier 설정 | ✅ 필수 (이미 포함됨)          |
| **Sensitive info types**                      | 주민번호, 여권번호 등 민감정보 탐지             | ⚪️ 이번 시나리오에는 불필요       |
| **Keywords or phrases**                       | 특정 키워드 기반 탐지                     | ⚪️ 필요 시 조직 내 금칙어 추가 가능 |
| **Communication size or attachment presence** | 메시지 크기, 첨부 파일 여부 기반 필터링          | ⚪️ 이번 시나리오와 무관         |

* 특정 키워드 추가
Add condition > Content contains keywords or phrases

<img width="960" alt="image" src="https://github.com/user-attachments/assets/d1297c3d-33ab-4385-983e-ac0c4ac1263c" />

### 🔗 [Step 4] Insider Risk Management Trigger 연계

Communication Compliance Policy 생성 후 ➔ **Insider Risk Management > Mod3 에서 생성한 IRM Policy를 edit  > Triggering event** 설정 단계에서:

✅ **Inappropriate messages detected by Communication Compliance** 선택  
➔ **Offensive language 탐지 시 IRM 정책 발동 ➔ Risk Score 할당 ➔ Adaptive Protection Enforcement 연계**


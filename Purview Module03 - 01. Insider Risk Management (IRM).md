# Purview Module 03 - Insider Risk Management

## Lab 1. Insider Risk Management (IRM)

### 시나리오 
- **Confidential – Wandoo 라벨**이 적용된 문서를
  - 외부로 메일 전송 시 **Risk alert 생성**
  - 특정 그룹(Wandoo-Security) 예외
  - 민감정보(Sensitive Info Types) 탐지 시 관리자 승인 및 알림
 

#### [Step 1] Microsoft Purview 포털 접속
Purview console > Solutions > Insider Risk Management > Policies > + Create policy > custom > **Choose a template** 화면에서 **Data leaks by risky users** 템플릿 선택

<img width="1405" alt="스크린샷 2025-06-29 오전 9 39 54" src="https://github.com/user-attachments/assets/84fdcfe0-860c-4dbe-9339-a84b972f78c3" />

#### [Step 2] Policy name & description

1. Name: Wandoo – Confidential External Email IRM
2. Description: Detects external email of Confidential – Wandoo labeled files with sensitive info
3. User: All
4. Exception: **Wandoo-security** group 추가
   
<img width="1397" alt="image" src="https://github.com/user-attachments/assets/512fc450-1307-461a-afbd-6e7649ce0de9" />

#### [Step 3] 우선순위 설정

<img width="1421" alt="image" src="https://github.com/user-attachments/assets/92e6dac0-0041-4092-b568-d4d2bc462c03" />

> ⭐️ Tips. 우선순위 설정
> 
> 내부자 위협 정책의 핵심은 ‘어떤 데이터를 보호할 것인가’를 정의하여, 우선순위 설정을 통해 조직의 중요 데이터 보호 정책에 집중 가능. 설정하지 않으면, 탐지 범위는 유지되지만, 중요도(Severity) 점수와 Alert 생성 가능성이 현저히 낮아짐 ➔ 보안 이벤트가 묻혀버릴 가능성 있음 

1. 설정

   ✅ 반드시 설정할 항목
   * Sensitivity labels: Confidential, Highly Confidential 등
   * Sensitive info types: 주민번호, 여권번호, 카드번호, 계좌번호
   * Trainable classifiers: 계약서, HR 문서, 재무 보고서 등

   ⚠️ 선택적 설정
   * File extensions: zip, csv, pst 등 특정 확장자 파일만 중요하면 선택
   * SharePoint sites: 특정 부서만 모니터링한다면 선택

3. Sharepoint 설정

<img width="1000" alt="image" src="https://github.com/user-attachments/assets/84102bd8-a5bf-44f8-abf7-466c7cb48108" />

| 옵션 | 의미 | 설정 가이드 |
| --- | --- | --- |
| **✔️ 특정 사이트 선택** | 선택된 SharePoint 사이트에서 발생하는 활동(다운로드, 복사 등)은 **Risk Score가 높게 책정**됩니다. | 조직에서 **민감자료, 기밀 문서, 중요 프로젝트**가 저장된 사이트를 선택하세요.<br>예) Wandoo Sales, Mark 8 Project Team |
| **❌ 선택하지 않음** | SharePoint 사이트 기반 우선순위가 적용되지 않음. | 민감정보 탐지는 계속 되지만, **위험도 우선순위가 낮아져 알림 생성 빈도가 줄어듦** |

- **설정:**
  - Wandoo Sales
  - Mark 8 Project Team
  - Benefits (인사/급여 관련 데이터 포함 시)

이렇게 설정하면: 위 사이트에서 **민감정보 다운로드, 복사, 공유** 등의 행동 탐지 시 ➔ **더 높은 Risk Score 부여 ➔ Alert 생성 ➔ 보안팀 대응 강화**

> ⭐️ Tips. 주의 사항
> 1. **최대 50개 사이트**까지 선택 가능
> 2. 정책 생성 후에도 수정 가능
> 3. 실제 선택 여부는 조직의 **데이터 분류 및 보호 대상 정의** 기준에 따를 것

3. Sensitivity Labels 설정

민감도 라벨(Sensitivity Labels)이 적용된 파일이나 이메일을 **우선 보호 대상으로 지정** ➔ 해당 라벨이 붙은 콘텐츠에서 이벤트 발생 시 **높은 Risk Score** 부여 ➔ **보호가 필요한 라벨**을 선택 후 **[Add]** 클릭
   - Confidential – Wandoo
   - Highly Confidential – Finance

> ⭐️ Tips. 권장 설정 시나리오
> - 조직의 기밀 문서(예: IRM 보호 문서, 외부 공유 제한 문서)에 Confidential 이상 라벨이 붙어있다면, 해당 라벨을 선택
> - 예시: **Confidential – Wandoo** 라벨 선택 ➔ 이 라벨이 붙은 문서를 다운로드, 업로드, 공유 등 이벤트 시 **High severity alert** 생성 가능

4. Sensitive Info Types 설정

주민등록번호, 여권번호, 신용카드번호 등 **민감정보(Sensitive Info Types)** 가 탐지된 콘텐츠를 우선 보호 대상으로 지정 ➔ 보호가 필요한 민감정보 타입을 선택 후 **[Add]** 클릭
   - Korea Resident Registration Number (주민등록번호)
   - South Korea Passport Number (여권번호)
   - Credit Card Number (신용카드번호)

> ⭐️ Tips. 권장 설정 시나리오
> - 주민등록번호, 여권번호 등 **법적 규제 대상 민감정보** 유출을 우선 탐지해야 할 경우
> - 예시: 주민등록번호 + 여권번호 + 신용카드번호 선택 ➔ 해당 정보가 포함된 콘텐츠의 활동(Event) 발생 시 **높은 Risk Score** 계산 ➔ 즉시 보안팀 대응 가능

5. Scoring
이 정책에서 탐지된 모든 활동에 대해 Risk Score를 계산할지, 아니면 Priority Content(우선순위 지정 콘텐츠) 가 포함된 활동만 점수 계산 및 Alert 생성할지를 결정.

<img width="1415" alt="image" src="https://github.com/user-attachments/assets/9c24c1e6-bd00-4ad5-88bf-d749f1579087" />

| 옵션                                                                | 설명                                                                                                                                                      | 권장 시나리오                                                        |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| **① Get alerts for all activity**                                 | ➔ 모든 탐지된 활동에 대해 Risk Score 부여 및 Alert 생성<br>- Priority content 포함 여부 관계없이<br>- 더 많은 Alert 발생 가능                                                         | ✅ **초기 모니터링 단계**<br>위험 사용자의 전반적 활동 패턴 파악 필요 시                  |
| **② Get alerts only for activity that includes priority content** | ➔ Priority content(SharePoint sites, Sensitivity labels, Sensitive info types 등) 포함 활동만 Risk Score 계산 및 Alert 생성<br>- Priority content가 없는 활동은 점수 계산 제외 | ✅ **운영 안정화 단계**<br>중요 콘텐츠 관련 유출/위험만 탐지해 false positive 감소 목표 시 |

본 랩에서는 우선 **Get alerts for all activity** 선택하여 탐지 범위 넓히는 설정 진행 

6. Trigger
Insider Risk Management 정책에서 어떤 이벤트가 발생했을 때 사용자의 리스크 점수를 계산하기 시작할지 정의하는 단계입니다. IRM 정책은 Scope(대상 사용자) 에 포함된 사람 모두를 항상 감시하는 것이 아니기 떄문에,반드시 Triggering Event(트리거 이벤트)가 발생해야 합니다. 이번 설정은 Module 4에서 **Communication Compliance** 생성 후 선택하여 진행합니다. 

| 트리거 옵션                                                          | 설명                                            | 현재 상태  | 활성화 조건                              |
| --------------------------------------------------------------- | --------------------------------------------- | ------ | ----------------------------------- |
| **Inappropriate messages detected by communication compliance** | 사용자 메시지에서 부적절한(욕설, 차별, 위협) 표현 탐지 시 정책 Trigger | ❌ 비활성화 | Communication Compliance 정책 선 생성 필요 |
| **HR data connector events**                                    | HR 시스템에서 퇴사, 징계 등 이벤트 발생 시 정책 Trigger         | ❌ 비활성화 | HR 커넥터 구성 필요                        |

<img width="1375" alt="스크린샷 2025-06-29 오전 10 04 15" src="https://github.com/user-attachments/assets/56df6134-ea87-4c07-beb6-427b1d3ca845" />

#### [Step 4] Indicator 설정

##### IRM 정책의 Alert 생성 원리
1. 트리거(Triggering event) 발생 → 정책 활성화 (ex. 부서 이동, 퇴사 예정, Communication compliance 등)
2. Indicator 조건 충족 → Risk score 할당
3. Threshold 초과 시 → Alert → Investigation → Response

##### Indicator: 	IRM 정책이 Risk alert를 생성하기 위한 ‘행동 이벤트 조건’ 

> ⭐️ 해당 부분이 붉은색으로 되어있으면, 클릭 후 활성화 
<img width="793" alt="image" src="https://github.com/user-attachments/assets/779662ee-5159-4666-8683-f882b7723777" />

| ✅ **구분** | **Indicator 이름** | **설명 / 목적** |
| --- | --- | --- |
| 🔴 **필수 (시나리오 핵심)** | Sending email with attachments to recipients outside the organization | Confidential 라벨 문서를 외부로 메일 전송 시 탐지 및 Risk Alert 생성 |
| 🟠 **강력 추천 (유출 우회 경로 차단)** | Removing sensitivity labels from files | 라벨 제거를 통한 보호 해제 시도 탐지 |
|  | Downgrading sensitivity labels applied to files | 라벨 보안 레벨 하향 변경 시 탐지 |
|  | Accessing sensitive or priority SharePoint files | 기밀 문서 열람/접근 탐지 |
|  | Downloading content from SharePoint / OneDrive | 기밀 파일 다운로드 후 재업로드/전송 시도 탐지 |
| 🟢 **옵션 (추가 보안)** | Sending email with attachments to free public domains | Gmail, Naver 등 개인 메일 전송 탐지 |
|  | Sending email with attachments to self | 개인 계정으로 전송 탐지 |
|  | Sharing SharePoint files/folders/sites externally | SharePoint 문서, 폴더, 사이트 외부 공유 탐지 |

위 Indicators 는 메일 외부 전송 뿐 아니라 우회 경로까지 탐지 가능 하므로, 이번 랩에서 설정 후 알림/리스크 스코어링 흐름을 확인하는 것을 권장합니다.
* 파일 다운로드 → 재업로드
* 라벨 제거 → 공유

#### [Step 5] Detection options (Sequence detection) 설정 

#### Sequence detection  
7일 기간 내에 두 가지 이상의 특정 활동이 순차적으로 발생하면 이를 고위험 행동으로 감지하는 기능

> ⭐️ 예시
>
> Sequence detection: Download from Microsoft 365 location then exfiltrate
> 사용자가 M365에서 파일을 다운로드 ➔ 외부로 유출하면 리스크 이벤트로 탐지


> ⭐️ 단일 Indicator 설정을 별도로 구성한 경우:
>
> Indicators 단계에서 “Download files from SharePoint or OneDrive” 같은 단일 indicator를 활성화하면 다운로드만으로도 alert이 생성될 수 있습니다.

> ⭐️Sequence detection이 아닌 단일 이벤트 탐지 정책을 사용한 경우:
>
> Insider Risk Policy의 Indicator 설정에서 단일 행동을 감시하도록 구성 시 가능

> ⭐️ DLP 정책과의 차이점
>
> DLP는 단일 다운로드도 조건 충족 시 alert 생성 가능, Insider Risk는 기본적으로 연속된 위험 시퀀스를 활용
> 
| 옵션 | 설명 | 시나리오 적합도 |
| --- | --- | --- |
| **Download from Microsoft 365 location then exfiltrate** | M365 (SharePoint, OneDrive)에서 파일 다운로드 후 외부 유출 시 탐지 | ⭐⭐⭐⭐⭐ (필수) |
| Download + Obfuscate + Exfiltrate | 다운로드 후 파일 암호화/변경 및 외부 유출 시 탐지 | ⭐⭐⭐ (권장) |
| Download + Exfiltrate + Delete | 다운로드 후 유출 후 삭제 시 탐지 | ⭐⭐⭐ (권장) |
| Archive then exfiltrate | 파일 압축 후 외부 유출 시 탐지 | ⭐⭐ (옵션) |
| Downgrade/remove label then exfiltrate | 라벨 다운그레이드 또는 제거 후 외부 유출 시 탐지 | ⭐⭐⭐⭐⭐ (필수) |

#### Cumulative exfiltration detection
사용자의 데이터 유출(exfiltration) 활동이 조직 내 평균 수준을 초과할 때 탐지
➔ 예: 특정 사용자가 지난 30일간 다른 사용자 대비 비정상적으로 많은 파일을 공유/다운로드 했을 경우

#### Risk score boosters
정책 탐지 시 Risk score(위험 점수)를 추가로 높여주는 조건
➔ 예: Confidential – Wandoo 라벨 문서 외부 전송을 탐지 시, 해당 사용자가 평소보다 많은 파일을 처리하면 위험도 우선 대응 가능

<img width="952" alt="image" src="https://github.com/user-attachments/assets/8045f8c5-e708-48ac-85d6-571707a9fea0" />

#### Indicator Threshold = 경고를 생성할 기준치로 MS 제공 기준을 그대로 사용
예: ‘외부 메일 첨부 전송’이라는 Indicator가 있을 때, 하루에 몇 건 이상이면 risk score를 높일 것인지를 정함

<img width="1410" alt="스크린샷 2025-06-29 오전 10 32 26" src="https://github.com/user-attachments/assets/ab9ac920-5315-4341-b780-80d47c99cf93" />

### 🔗 [다음 Lab으로 이동하기 »](https://github.com/Kittiyayaong/ProjectWandooPurview/blob/main/Purview%20Module04%20-%2001.%20Communication%20Compliance.md)

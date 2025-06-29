# Purview Module 03 - Insider Risk Management

## Lab 1. Insider Risk Management (IRM).md

### 시나리오 
- **Confidential – Wandoo 라벨**이 적용된 문서를
  - 외부로 메일 전송 시 **Risk alert 생성**
  - 특정 그룹(`Wandoo test group`)은 예외 처리
  - 민감정보(Sensitive Info Types) 탐지 시 관리자 승인 및 알림
 

#### [Step 1] Microsoft Purview 포털 접속
Purview console > Solutions > Insider Risk Management > Policies > + Create policy > custom > **Choose a template** 화면에서 **Data leaks by risky users** 템플릿 선택

<img width="1405" alt="스크린샷 2025-06-29 오전 9 39 54" src="https://github.com/user-attachments/assets/84fdcfe0-860c-4dbe-9339-a84b972f78c3" />

#### [Step 2] Policy name & description

1. Name: Wandoo – Confidential External Email IRM
2. Description: Detects external email of Confidential – Wandoo labeled files with sensitive info
3. User: All 

<img width="1436" alt="스크린샷 2025-06-29 오전 9 42 52" src="https://github.com/user-attachments/assets/4da0bc5f-9bc7-41e7-9d92-2b5e74ee90e1" />

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

2. Sharepoint 설정

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

민감도 라벨(Sensitivity Labels)이 적용된 파일이나 이메일을 **우선 보호 대상으로 지정** ➔ 해당 라벨이 붙은 콘텐츠에서 이벤트 발생 시 **높은 Risk Score** 부여
   - Confidential – Wandoo
   - Highly Confidential – Finance
4. **보호가 필요한 라벨**을 선택 후 **[Add]** 클릭

> ⭐️ Tips. 권장 설정 시나리오
> - 조직의 기밀 문서(예: IRM 보호 문서, 외부 공유 제한 문서)에 Confidential 이상 라벨이 붙어있다면, 해당 라벨을 선택
> - 예시: **Confidential – Wandoo** 라벨 선택 ➔ 이 라벨이 붙은 문서를 다운로드, 업로드, 공유 등 이벤트 시 **High severity alert** 생성 가능

---

### 🔷 **Sensitive Info Types**

#### ✅ **화면 설명**
- **위치:** Content to prioritize 단계 > Sensitive info types 선택
- **목적:**  
  주민등록번호, 여권번호, 신용카드번호 등 **민감정보(Sensitive Info Types)** 가 탐지된 콘텐츠를 우선 보호 대상으로 지정

#### ✅ **설정 방법**
1. **[Add or edit Sensitive info types]** 클릭  
2. Microsoft Purview 내 정의된 Sensitive Info Types 리스트가 표시됨
3. 예:
   - Korea Resident Registration Number (주민등록번호)
   - South Korea Passport Number (여권번호)
   - Credit Card Number (신용카드번호)
4. 보호가 필요한 민감정보 타입을 선택 후 **[Add]** 클릭

#### ✅ **권장 설정 시나리오**
- 주민등록번호, 여권번호 등 **법적 규제 대상 민감정보** 유출을 우선 탐지해야 할 경우
- 예시: 주민등록번호 + 여권번호 + 신용카드번호 선택 ➔  
  해당 정보가 포함된 콘텐츠의 활동(Event) 발생 시 **높은 Risk Score** 계산 ➔ 즉시 보안팀 대응 가능

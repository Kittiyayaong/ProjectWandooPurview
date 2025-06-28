# Purview Module 02. Data Loss Prevention

## Lab 1. Template-based Data Loss Prevention 

### ✅ 설정하기 (Template base) 

1. Process

![image](https://github.com/user-attachments/assets/ece16377-b91a-4956-b9b7-5a93fc720ea6)

2. 설정 위치

Purview console > Solutions > Data Loss Prevention > Policies > + Create policy

![image](https://github.com/user-attachments/assets/fb23fcba-5bda-4f5c-969e-4a5f6c2f2bd8)

3. Template-based Policy: GDPR을 예로 진행 (Enhanced > GDPR Enhanced > next > policy name setting > next) 

![image](https://github.com/user-attachments/assets/d132f61e-1b95-4514-8a6b-fdf9d031aab4)

Tips.Enhanced templates은 온프레미스 파일 저장소, Power BI, Azure Storage, Azure SQL Server, AWS S3, OpenAI ChatGPT, Google Gemini, Microsoft Bing Chat 위치에서는 사용할 수 없습니다.

4. admin unit 설정하기 (참고 – 이번 Lab에서는 설정하지 않습니다.Entra에서 사전 설정된 Admin unit을 사용합니다.)

* Admin Units?

Admin Units는 Microsoft Entra ID에서 다른 Microsoft Entra 리소스(예: 사용자, 그룹, 장치)를 위한 설정입니다. 조직의 특정 부분에 대한 권한을 제한하는 데 사용됩니다. 예를 들어, 지역 지원 전문가에게 Helpdesk Administrator 역할을 위임하여 그들이 지원하는 지역의 사용자만 관리할 수 있도록 할 수 있습니다

![image](https://github.com/user-attachments/assets/02bba716-892f-4d48-909b-8f4b1249da52)

5. policy를 적용 대상 선택 

![image](https://github.com/user-attachments/assets/ecd8f0a4-c8a3-49a8-bc10-2801187393ce)

6. Policy setting

![image](https://github.com/user-attachments/assets/f61772d2-bbff-4cda-9b25-83236a457059)

* 템플릿의 기본 설정 검토 및 사용자 지정:선택한 템플릿의 기본 설정을 검토하고 필요한 경우 사용자 지정할 수 있습니다. 기본 설정을 빠르게 설정하여 정책을 구성할 수 있는 방법입니다. 예를 들어, 금융 데이터, 개인 식별 정보(PII), 건강 정보, GDPR 관련 정보 등의 템플릿을 사용할 수 있습니다. 이러한 템플릿은 이미 설정된 규칙과 조건을 포함하고 있어, 빠르게 DLP 정책을 설정할 수 있도록 도와줍니다.
* 고급 DLP 규칙 생성 또는 사용자 지정:  고급 DLP 규칙을 생성하거나 기존 규칙을 사용자 지정할 수 있습니다. 더 세부적으로 조정하고 특정 요구 사항에 맞게 설정할 수 있습니다. 예를 들어, 특정 조건을 추가하여 민감한 정보가 포함된 이메일을 차단하거나, 특정 사용자 그룹에만 적용되는 규칙을 만들 수 있습니다. 또한, 고급 규칙을 사용하면 민감도 레이블을 적용하고, 특정 파일 형식이나 위치에 따라 규칙을 설정할 수 있습니다

7. GDPR 템플릿의 기본 설정값
   
![image](https://github.com/user-attachments/assets/269eeb27-ad6d-4419-89ec-4ca2cbda4c53)

8. DLP 설정하기 –  policy settingGDPR template 기본 설정 내용 변경 및 추가

Group 여러 개 설정 가능하며, 각 Group 항목별로 confidence 설정 가능 (예시에서는 Group명을 confidence level로 설정)  

![image](https://github.com/user-attachments/assets/28562135-d38d-4c3c-88b6-ef283025920b)

Tips. instance count는 Microsoft Purview DLP 정책 설정에서 특정 유형의 민감한 정보가 감지되어 정책이 적용되기 위해 필요한 발생 횟수를 의미합니다. 인스턴스 수가 많아질수록 정책이 더 민감하게 작동하여, 더 많은 민감한 정보가 감지될 때 정책이 적용됩니다
Medium Confidence: 예를 들어, "Medium Confidence"를 10으로 설정하면, 특정 유형의 민감한 정보가 10번 감지될 때 정책이 적용됩니다.
High Confidence: "High Confidence"를 5로 설정하면, 특정 유형의 민감한 정보가 5번 감지될 때 정책이 적용됩니다. "any"로 설정하면, 민감한 정보가 한 번이라도 감지되면 정책이 적용됩니다.

9. Protection actionspolicy의 protection actions

DLP(Data Loss Prevention) 정책에서 특정 조건이 충족되었을 때 수행되는 조치

![image](https://github.com/user-attachments/assets/f9d3f585-6dc3-4b37-a9bb-c15cd0f387be)

* 특정 양의 민감한 정보가 한 번에 공유될 때 감지:한 번에 공유되는 특정 양의 민감한 정보를 감지하는 설정입니다. 예를 들어, 동일한 민감한 정보 유형의 인스턴스가 10개 이상일 때 감지하도록 설정할 수 있습니다.
* 이메일로 사고 보고서 전송: 기본적으로 사용자와 글로벌 관리자가 이메일로 사고 보고서를 자동으로 받게 됩니다. 사고 보고서는 Exchange, SharePoint, OneDrive, Teams에서의 활동에 대해서만 지원됩니다. 보고서에 포함할 내용과 수신자를 선택할 수 있습니다.
* DLP 규칙이 일치할 경우 경고 전송: 기본적으로 사용자와 글로벌 관리자가 DLP 규칙이 일치할 경우 자동으로 경고를 받게 됩니다. 경고 구성은 사용자 정의할 수 있습니다.
* Microsoft 365 위치에서 콘텐츠 접근 제한 또는 암호화: Microsoft 365 위치에서 콘텐츠의 접근을 제한하거나 암호화하는 설정입니다.

10. 사고 보고서(incident reports) 설정
    
정책 일치가 발생했을 때 사용자에게 알림을 보내는 방법을 구성할 수 있습니다.

![image](https://github.com/user-attachments/assets/e8c3ccd0-96dd-4b9d-9130-e7bbc3058adf)

* 특정 사람에게 알림 보내기: "Send notifications to these people" 아래에 사용자를 추가하거나 제거하여 특정 사람에게 알림을 보낼 수 있습니다.

11. 경고(alert) 설정
특정 사람에게 이메일 경고 보내기 (선택 사항): "Add or remove groups＂를 통해 특정 사람이나 그룹에게 이메일 경고를 보낼 수 있습니다.

![image](https://github.com/user-attachments/assets/fe139b7b-704b-4724-89e3-d0ab5cc84abf)

### 경고 빈도 옵션:

* Send alert every time an activity matches the rule: 규칙과 일치하는 활동이 있을 때마다 경고 보내기
* Send alert when the volume of matched activities reaches a threshold: 일치하는 활동의 양이 임계값에 도달할 때 경고 보내기
* 임계값 설정
  1. Instances more than or equal to: 인스턴스가 -개 이상일 때)
  2. Volume more than or equal to: 용량이 -MB 이상일 때
* 시간 프레임 및 사용자 범위:
  1. During the last: -분 동안
  2. For: 대상 설정 (전체: all user/ 인당: single user) 

12. Customize access and override settings

Override는 DLP(Data Loss Prevention) 정책에서 특정 조건이 충족되었을 때 사용자가 정책의 제한을 무시할 수 있도록 허용하는 기능입니다. 예를 들어, 사용자가 민감한 정보를 포함하는 이메일을 보내거나 파일을 공유하려고 할 때, DLP 정책이 이를 차단할 수 있습니다. 하지만 사용자가 정책을 무시하고 계속 진행할 수 있도록 허용하는 옵션이 있습니다.

![image](https://github.com/user-attachments/assets/c9d3d418-5439-4ef8-a990-5a490a7be12e)


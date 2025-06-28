# Purview Module 01. Information Protection

## Lab 5. Auto-labeling

1. Auto-labeling이란?

Microsoft Purview의 자동 라벨링(auto-labeling)은 민감한 정보를 자동으로 분류하고 보호하기 위해 설계된 기능입니다. 관리자가 설정한 조건에 따라 파일, 이메일, 문서 등에 민감도 라벨을 자동으로 적용합니다. 이를 통해 사용자가 직접 라벨을 적용할 필요 없이 파일과 이메일에 라벨을 자동으로 적용하며, 사용자가 문서를 저장하기 전에 라벨을 적용할 수 있습니다
예를 들어, Microsoft Purview Information Protection에서는 클라이언트 측 자동 라벨링을 통해 사용자가 문서를 편집하거나 이메일을 작성할 때 민감도 라벨을 자동으로 적용할 수 있습니다. 또한, 서비스 측 자동 라벨링을 통해 SharePoint, OneDrive, Exchange Online에 저장된 문서나 이메일에 라벨을 적용할 수 있습니다

### 자동 라벨링을 위한 두가지 방법 

* 클라이언트 측 라벨링: 클라이언트 측 라벨링은 사용자가 문서를 편집하거나 이메일을 작성할 때 민감도 라벨을 자동으로 적용하는 방식입니다. 이 방식은 사용자가 파일을 생성하거나 수정할 때 실시간으로 라벨을 적용합니다. 예를 들어, 사용자가 5개의 신용카드 번호를 포함하는 파일을 열거나 생성하면, 해당 파일에 자동으로 라벨이 적용됩니다.클라이언트 측 라벨링은 Office 애플리케이션 내에서 작동하며, 사용자가 라벨을 추천받거나 자동으로 적용할 수 있습니다1
* 서비스 측 라벨링: 서비스 측 라벨링은 SharePoint, OneDrive, Exchange Online에 저장된 문서나 이메일에 라벨을 적용하는 방식입니다. 이 방식은 데이터가 이미 저장된 상태에서 라벨을 적용하며, 데이터가 이동 중일 때도 적용될 수 있습니다. 예를 들어, SharePoint나 OneDrive에 저장된 문서나 Exchange Online을 통해 송수신되는 이메일에 라벨이 적용됩니다.서비스 측 라벨링은 사용자가 어떤 애플리케이션을 사용하든 상관없이 조직 전체에서 즉시 사용할 수 있으며, 대규모 라벨링에 적합합니다.

2. 설정 위치
   
Purview console > solution > Information protection > sensitivity label > 작성된 라벨 선택 후 edit > auto-labeling 설정으로 진입  

![image](https://github.com/user-attachments/assets/4fb52954-1abf-456d-9ec8-aca90b40f447)

3. Template Auto-labeling 설정 전 사전 설정 : Audit 기능 활성화 (참고)
   
Purview console > Solution > Audit > Start recording user and admin activity 클릭 후 활성화 

![image](https://github.com/user-attachments/assets/bd2c75d1-5fb6-42b7-97ac-840c013810a7)

Tip.템플릿 기반 설정: 템플릿 기반 설정을 사용할 때는 감사 로그를 활성화해야 합니다. 템플릿을 기반으로 한 자동 라벨링 정책이 조직의 보안 및 규정 준수 요구사항을 충족하기 위해 더 정교한 추적과 모니터링이 필요하기 때문입니다

4. Template Auto-labeling 설정하기 – Template 기반 (참고)

Purview console > Solution > Information Protection > Policies > Auto-labeling policies > +Create auto-labeling policy

![image](https://github.com/user-attachments/assets/e6aa1462-4efc-424b-9ea5-3f57f7be780a)

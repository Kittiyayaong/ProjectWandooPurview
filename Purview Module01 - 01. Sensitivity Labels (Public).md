# Purview Module 01. Information Protection

## Lab 1. Sensitivity labels (Public) 

### Sensitivity labels이란?
민감한 정보 분류 및 보호를 위한 테그

![image](https://github.com/user-attachments/assets/44eea4a5-300a-483a-94d1-f719e9301a07)

1. Sensitivity Labels (SLs) across workloads

![image](https://github.com/user-attachments/assets/835011f8-ec98-4f7e-899c-93fb067a6567)

* Public Label: 공공 소비를 위해 설계된 데이터를 나타냅니다.
* General Label: 공공 소비를 위한 것이 아닌 비즈니스 데이터를 나타냅니다.
* Confidential: 과도하게 공유될 경우 비즈니스에 피해를 줄 수 있는 민감한 비즈니스 데이터를 나타냅니다.
* Restricted: 매우 민감한 비즈니스 데이터를 나타내며, 이는 과도하게 공유될 경우 비즈니스에 피해를 줄 수 있습니다.

2. Sensitivity labels(SL)의 유형: 각기 다른 데이터 보호 요구 사항을 충족하고, 조직 내에서 민감한 정보를 효과적인 관리를 제공합니다.

![image](https://github.com/user-attachments/assets/aa40007a-bb6b-4c9c-8874-83801c3b7a1e)

### ✅ Public SL 설정하기 
1. 설정위치
Purview console (purview.microsoft.com) > Information protection >  Sensitivity Labels 	

![image](https://github.com/user-attachments/assets/b669f87b-b806-49ea-a0c5-7cd2a0c6e3a9)

2. Label 정보 

![image](https://github.com/user-attachments/assets/c5bf863a-4458-49ed-8a16-e84165e062e8)

* Personal: 개인적인 용도로 사용되는 데이터에 적용됩니다. 우선순위는 가장 낮습니다.
* General: 일반적인 비공개 데이터에 적용됩니다. 내부 직원, 비즈니스 게스트 및 외부 파트너와 공유할 수 있습니다.
* Anyone (unrestricted): 제한 없이 누구와도 공유할 수 있는 데이터에 적용됩니다.
* All Employees (unrestricted): 모든 직원과 제한 없이 공유할 수 있는 데이터에 적용됩니다.
* Confidential: 기밀 데이터에 적용됩니다. 인증된 사용자만 접근할 수 있습니다.
* All Employees: 모든 직원과 공유할 수 있는 데이터에 적용됩니다.
* Confidential Employees: 기밀 데이터를 다루는 직원에게만 적용됩니다.
* Trusted People: 신뢰할 수 있는 사람들과만 공유할 수 있는 데이터에 적용됩니다.
* Highly Confidential: 매우 기밀 데이터에 적용됩니다. 조직 내 특정 사용자만 접근할 수 있습니다.
* Specified People: 지정된 사람들과만 공유할 수 있는 데이터에 적용됩니다.
* All Employees (specified): 지정된 모든 직원과 공유할 수 있는 데이터에 적용됩니다. 조직 내 모든 임직원이 접근할 수 있어야 하는 중요한 정보를 보호하기 위해 사용됩니다. 예를 들어, 회사의 정책, 절차, 내부 통신 등 모든 임직원이 알아야 할 중요한 정보가 포함

3. Label Priority
라벨의 우선순위(priority)는 민감도 라벨 정책의 적용 순서를 나타냅니다. 우선순위가 높은 라벨일수록 더 중요한 데이터에 적용되며, 정책 충돌 시 우선순위가 높은 라벨의 설정이 적용됩니다

4. Public Label 설정하기: 공공 소비를 위해 설계된 데이터를 나타냅니다 

![image](https://github.com/user-attachments/assets/689aad47-087a-4616-91b6-b5c538d90b01)

> ⭐️ Tips.
>
> 라벨 우선순위는 기본적으로 가장 높은 우선순위로 설정됩니다. 이는 사용자가 라벨을 생성할 때 기본값으로 설정되지만, 생성 후에 변경할 수 있습니다.
기본값으로 가장 높은 우선순위가 설정되는 이유는 새로운 라벨이 생성될 때 해당 라벨이 중요한 데이터에 적용될 가능성이 높기 때문입니다. 하지만 필요에 따라 관리자가 우선순위를 조정하여 다른 라벨과의 충돌을 방지하고, 데이터 보호 정책을 효과적으로 적용할 수 있습니다.

5. Scope 설정하기: Public Label 설정 가능한 범위
* 파일 및 기타 데이터 자산: Microsoft 365, Microsoft Fabric(포함 Power BI), Microsoft Azure에서 파일 및 데이터 자산에 라벨을 적용합니다.
* 이메일: 모든 버전의 Outlook에서 보낸 메시지에 라벨을 적용합니다.
* 회의: Outlook 및 Teams에서 일정 및 회의에 라벨을 적용합니다.
* 그룹 및 사이트: 라벨이 적용된 Teams, Microsoft 365 그룹, SharePoint 사이트 및 Loop 작업 공간을 보호하기 위해 프라이버시, 액세스 제어 및 기타 설정을 구성합니다

![image](https://github.com/user-attachments/assets/8a1e3be7-4dc2-4da4-82a4-80f446531303)

6. Item 설정하기
Microsoft 365에서 항목에 라벨을 적용할 때 사용할 보호 설정이며, 각 항목은 특정 보호 기능을 제공하며, 필요에 따라 선택할 수 있습니다.

* 액세스 제어: 라벨이 적용된 항목에 누가 접근하고 볼 수 있는지를 제어합니다.
* 콘텐츠 마킹 적용: 라벨이 적용된 항목에 사용자 정의 헤더, 푸터 및 워터마크를 추가합니다.
* Teams 회의 및 채팅 보호: Teams 회의 및 채팅에 대한 보호 설정을 구성합니다. 이 기능을 사용하려면 조직에 Teams Premium 라이선스가 필요합니다.

![image](https://github.com/user-attachments/assets/c4269a99-e3a2-46fd-97e1-2ffe1ed0b244)

7. Auto-labeling 설정 (이후 과정에서 다시 설정 예정)

![image](https://github.com/user-attachments/assets/332a365e-c9b5-47ee-80aa-bd2b8ea092ea)

> ⭐️ Tips. Auto-labeling?
>
> 특정 조건에 맞는 콘텐츠를 포함하는 Office 파일이나 이메일에 자동으로 라벨을 적용할 수 있습니다. 예를 들어, 회사에서 민감한 정보를 포함한 파일이나 이메일에 자동으로 민감도 라벨을 적용한다면, 민감한 정보는 예를 들어, 신용 카드 번호, 은행 계좌 번호 등이 될 수 있습니다. 회사에서 "기밀" 라벨을 생성하고, 사회 보장 번호나 신용 카드 번호가 포함된 모든 파일과 이메일에 이 라벨을 자동으로 적용하도록 설정하면 사용자가 직접 라벨을 적용하지 않아도, 민감한 정보가 포함된 모든 파일과 이메일에 자동으로 "기밀" 라벨이 적용되어 보호됩니다

8. Container SL 설정하기

![image](https://github.com/user-attachments/assets/c87a64dd-feb8-4fb9-b4ff-7584c666121e)

* 프라이버시 및 외부 사용자 액세스: 내부 및 외부 사용자가 라벨이 적용된 팀과 Microsoft 365 그룹에 접근할 수 있는 수준을 제어할 수 있습니다. 예를 들어, 외부 사용자의 접근을 제한하거나 특정 사용자만 접근할 수 있도록 설정할 수 있습니다.
* 외부 공유 및 조건부 액세스: 라벨이 적용된 SharePoint 사이트의 외부 공유를 제어하고 조건부 액세스 설정을 구성할 수 있습니다. 이를 통해 민감한 정보를 보호하고, 특정 조건을 만족하는 사용자만 접근할 수 있도록 할 수 있습니다.
* 비공개 팀 검색 가능성 및 공유 채널 설정: 이 설정을 통해 비공개 팀이 검색에서 발견될 수 있는지 여부를 결정하고, 공유 채널에 초대할 수 있는 팀 유형을 제어할 수 있습니다. 이를 통해 비공개 팀의 보안을 강화하고, 특정 팀만 공유 채널에 접근할 수 있도록 할 수 있습니다.

![image](https://github.com/user-attachments/assets/da1654d0-e9f5-4406-97b8-d4b721affb9a)

![image](https://github.com/user-attachments/assets/8b6f1a2c-4a2c-4aed-a7fe-6928d0a309f1)

> ⭐️ Tips.
>
>  Microsoft Entra 조건부 액세스를 사용하여 라벨이 지정된 SharePoint 사이트 보호 
라벨이 지정된 사이트에 대한 접근을 제어하는 데 사용됩니다. 이를 통해 관리되지 않는 장치에서 라벨이 지정된 SharePoint 사이트에 접근할 수 있는지 여부를 제어하거나, 리소스 테넌트에서 인증 컨텍스트를 적용하여 사이트 접근을 제한할 수 있습니다.

9. 설정 완료
    
![image](https://github.com/user-attachments/assets/aa087ea1-0426-4f83-aa89-51c1b06e3f85)

![image](https://github.com/user-attachments/assets/6d79b3b1-90d5-4a08-9900-c0886d369910)


### 🔗 [다음 Lab으로 이동하기 »](https://github.com/Kittiyayaong/ProjectWandooPurview/blob/main/Purview%20Module01%20-%2002.%20Sensitivity%20Labels%20(General).md)

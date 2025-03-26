# Purview Module 01. Information Protection

## Lab 4. Label Policy 

### Label Policy 란? 
라벨 정책은 민감도 라벨을 조직 내에서 어떻게 적용하고 관리할지를 정의하는 규칙입니다. 이를 통해 특정 데이터에 대한 보안 및 접근 제어를 설정할 수 있습니다. 예를 들어, 기밀 문서에 대한 접근 권한을 제한하거나, 특정 조건을 만족하는 사용자만 접근할 수 있도록 설정할 수 있습니다. 

1. 설정 위치: Purview console > Information protection > Policies > label Publishing policies 

![image](https://github.com/user-attachments/assets/48a7f867-ac21-4df7-b82b-956fe85505f3)

2. Assign Admin Units (이번 Lab에는 미설정합니다)

라벨 정책을 특정 사용자나 그룹에만 적용할 수 있도록 관리 단위를 지정하는 기능입니다. 관리 단위는 Microsoft Entra ID에서 생성되며, 정책을 특정 사용자나 그룹에 제한하는 데 사용됩니다.

* 관리 단위 (Admin Units): 관리 단위는 조직 내 특정 사용자나 그룹을 포함하는 단위입니다.이를 통해 정책을 특정 사용자나 그룹에만 적용할 수 있습니다.예를 들어, 특정 부서나 팀에만 정책을 적용하고자 할 때 유용합니다. 모든 위치에서 지원되지 않습니다. 예를 들어, Fabric 및 Microsoft 365 Copilot과 같은 위치에서는 관리 단위를 선택할 수 없습니다.

![image](https://github.com/user-attachments/assets/1c74f484-cd33-483b-bbb9-ca20084a8fbd)

3. Publish to Users and Groups (이번 Lab에는 미설정합니다.)
선택한 민감도 라벨을 사용자, 배포 그룹, 메일 사용 보안 그룹 및 Microsoft 365 그룹에서 사용할 수 있도록 설정하는 기능입니다. 이를 통해 조직 내 특정 사용자나 그룹이 민감도 라벨을 적용하고 사용할 수 있게 됩니다.

![image](https://github.com/user-attachments/assets/603e2a4a-23e2-4092-8c15-55471bbbf64c)

* Assign Admin Units: 인사팀과 법무팀에만 "Confidential View Only" 라벨을 적용합니다. 이를 통해 해당 부서의 사용자만 해당 라벨을 사용할 수 있게 제한합니다.
* Publish to Users and Groups: 인사팀과 법무팀의 모든 사용자와 그룹이 "Confidential View Only" 라벨을 사용할 수 있게 설정합니다.

4. Policy Setting

![image](https://github.com/user-attachments/assets/b9734bcb-ed31-4692-bf23-38af12ba781c)

* Users must provide a justification to remove a label or lower its classification: 이 설정을 활성화하면 사용자가 라벨을 제거하거나 낮은 등급의 라벨로 교체하기 전에 이유를 제공해야 합니다. 이를 통해 민감한 정보의 보호를 강화하고, 사용자가 라벨을 변경하는 이유를 기록할 수 있습니다. 예를 들어, 사용자가 기밀 문서에서 라벨을 제거하려고 할 때, "이 문서는 더 이상 기밀 정보가 아닙니다"와 같은 이유를 입력해야 합니다. 관리자는 활동 탐색기를 통해 사용자가 제공한 이유를 검토할 수 있습니다.
* Require users to apply a label to their emails and documents: 이 설정을 활성화하면 사용자가 문서를 저장하거나 이메일을 보내기 전에 라벨을 적용해야 합니다. 이는 문서와 이메일에 민감도 라벨을 적용하여 보안을 강화하는 데 도움이 됩니다. 예를 들어, 사용자가 새 이메일을 작성할 때, 보내기 전에 "Confidential" 라벨을 선택해야 합니다 
* Require users to apply a label to their Fabric and Power BI content: 이 설정을 활성화하면 사용자가 Fabric 및 Power BI에 콘텐츠를 저장하기 전에 라벨을 적용해야 합니다. 이를 통해 Fabric 및 Power BI 콘텐츠의 보안을 강화할 수 있습니다. 예를 들어, 사사용자가 Power BI 보고서를 작성할 때, 저장하기 전에 "Internal Use Only" 라벨을 선택해야 합니다.
* Provide users with a link to a custom help page: 이 설정을 통해 사용자가 라벨을 사용하는 방법에 대한 구체적인 도움말 페이지 링크를 제공할 수 있습니다. 예를 들어, 사용자가 라벨을 사용하는 방법에 대한 도움말 페이지 링크를 제공하여, 사용자가 라벨을 올바르게 적용하고 사용할 수 있도록 도울 수 있습니다. 

5. Default Settings for Documents

![image](https://github.com/user-attachments/assets/00c4a564-0dda-4a59-870d-40984e05e6d3)

* Default label:

기본 라벨을 선택하는 옵션입니다. 선택한 라벨이 Word, Excel, PowerPoint 문서가 생성되거나 수정될 때 자동으로 적용됩니다. 사용자는 문서의 민감도에 더 잘 맞는 다른 라벨을 선택할 수 있습니다.
회사에서 모든 새 문서에 기본적으로 "General - Wandoo" 라벨을 적용하도록 설정할 수 있습니다. 이렇게 하면 사용자가 새 문서를 작성할 때 자동으로 이 라벨이 적용되며, 필요에 따라 다른 라벨로 변경할 수 있습니다.

6. Default Settings for emails

![image](https://github.com/user-attachments/assets/f13a4221-94df-4669-bb32-eaa2f4f03169)

* Default label:

이메일에 기본 라벨을 적용하는 기능입니다. 선택한 라벨이 새 이메일과 기존의 라벨이 없는 이메일에 자동으로 적용됩니다. 사용자는 이메일을 보내기 전에 기본 라벨을 변경할 수 있습니다

*Inherit label from attachments: 

이메일에 첨부된 파일의 라벨을 상속받을 수 있습니다. 사용자가 "General - Wandoo" 라벨이 적용된 새 이메일을 작성하고, "Confidential" 라벨이 적용된 문서를 첨부하면, 이메일은 자동으로 "Confidential" 라벨을 상속받아 보안을 강화할 수 있습니다. 

7. Default Settings for meetings and calendar events

![image](https://github.com/user-attachments/assets/0500633a-085f-4da8-8cf5-a34e092e256d)

* Default label

회의 및 캘린더 이벤트에 기본 라벨을 적용하는 기능입니다. 선택한 라벨이 새 회의와 기존의 라벨이 없는 캘린더 이벤트에 자동으로 적용됩니다. 사용자는 이벤트나 회의를 생성하기 전에 기본 라벨을 변경할 수 있습니다.

* Apply inheritance between Teams meeting and artifacts

회의에 라벨이 지정된 후, 더 높은 우선순위의 라벨이 적용된 파일이 업로드되거나 회의에 공유되면, 회의의 라벨을 자동으로 해당 파일의 라벨로 교체하거나 사용자가 직접 변경하도록 권장할 수 있습니다.

8. Default Settings for sites and groups

![image](https://github.com/user-attachments/assets/8cf5786b-7400-458c-a6b3-41aac267e4bb)

* Default label:

SharePoint 사이트와 Microsoft 그룹에 기본 라벨을 적용하는 기능입니다. 선택한 라벨이 새로 생성된 라벨이 없는 SharePoint 사이트와 Microsoft 그룹에 자동으로 적용됩니다. 사용자는 사이트나 그룹을 생성하기 전에 기본 라벨을 변경할 수 있습니다.

* Require users to apply a label to their groups or sites

이 설정을 활성화하면 사용자가 그룹이나 사이트를 생성하기 전에 라벨을 적용해야 합니다. 이는 그룹과 사이트에 민감도 라벨을 적용하여 보안을 강화하는 데 도움이 됩니다.

9. Default Settings for Fabric and Power BI content

![image](https://github.com/user-attachments/assets/bd99acc8-5da9-4841-b50d-879750d444cc)

10. Policy name 및 설정완료

![image](https://github.com/user-attachments/assets/063c176a-aac6-4058-8e74-084348887471)


## Lab 3. Sensitivity labels (Confidential/Confidential-internal) 

### Confidential SL 설정하기 

1. Confidential Label: 과도하게 공유될 경우 비즈니스에 피해를 줄 수 있는 민감한 비즈니스 데이터를 나타냅니다.

2. Scope 설정하기
![image](https://github.com/user-attachments/assets/097e9229-9e07-44cb-a8a7-a264d54b8cfd)

3. Item 설정하기

![image](https://github.com/user-attachments/assets/d7a584a2-05b8-4bc1-b30e-9e8727ef5b97)

* 액세스 제어 (Control access): “접근제어” 라벨이 적용된 항목에 누가 접근하고 볼 수 있는지를 제어할 수 있습니다. 이를 통해 민감한 정보를 보호하고, 특정 사용자만 접근할 수 있도록 할 수 있습니다. 예를 들어, 기밀 문서가 외부로 유출되는 것을 방지하고, 내부 사용자 중에서도 필요한 사람만 접근할 수 있도록 제한할 수 있습니다. 
* 콘텐츠 마킹 적용 (Apply content marking): “민감도 인식“ 라벨이 적용된 항목에 사용자 정의 헤더, 푸터, 워터마크를 추가할 수 있습니다. 이를 통해 문서의 민감도를 시각적으로 표시하고, 정보 보호를 강화할 수 있습니다. 예를 들어, 문서 상단에 "Confidential"이라는 워터마크를 추가하여 문서가 기밀 정보임을 명확히 표시할 수 있습니다..
* Teams 회의 및 채팅 보호 (Protect Teams meetings and chats): Teams 회의 및 채팅에 대한 보호 설정을 구성할 수 있습니다. 이를 통해 민감한 정보가 포함된 회의와 채팅을 보호할 수 있습니다. 이 기능을 사용하려면 조직에 Teams Premium 라이선스가 필요합니다.

![image](https://github.com/user-attachments/assets/4566556a-52f5-4b36-9c14-a595a085d857)

### User Access to content expires 
라벨이 적용된 항목에 대한 사용자 접근 권한이 만료되는 시점을 지정하는 기능입니다.
* Never (만료되지 않음): 사용자가 콘텐츠에 영구적으로 접근할 수 있습니다.
* On a specific date (특정 날짜에 만료): 사용자가 콘텐츠에 접근할 수 있는 특정 날짜를 지정할 수 있습니다.
* A number of days after label is applied (라벨이 적용된 후 일정 일수 후에 만료): 라벨이 적용된 후 사용자가 콘텐츠에 접근할 수 있는 일수를 지정할 수 있습니다.

### Allow Offline Access
사용자가 콘텐츠를 오프라인으로 다운로드하고 볼 수 있는지를 지정하는 기능입니다. 또한, 오프라인 접근이 허용된 경우, 사용자가 오프라인으로 콘텐츠에 접근할 수 있는 기간을 설정할 수 있습니다. 예를 들어, 사용자가 콘텐츠를 오프라인으로 접근할 수 있는 일수를 30일로 설정할 수 있습니다
* User Access to Content Expires: 사용자가 온라인으로 콘텐츠에 접근할 수 있는 기간을 설정합니다.
* Allow Offline Access: 사용자가 콘텐츠를 오프라인으로 다운로드하고 볼 수 있는지를 설정하며, 오프라인 접근 기간을 지정합니다.

### Assign permission
라벨이 적용된 항목에 대해 사용자에게 부여할 권한을 지정하는 기능입니다. 이를 통해 각 사용자 역할에 따라 수행할 수 있는 작업을 제어할 수 있습니다.
* Internal/External 모두 조건에 맞는 인증만 된다면 접근 가능하기 때문에, ‘add any authenticated users’추가

![image](https://github.com/user-attachments/assets/d5f505cb-4842-4de8-b0c6-4c45f091624c)

### Contents marking
라벨이 적용된 콘텐츠에 사용자 정의 헤더, 푸터, 워터마크를 추가할 수 있는 기능입니다. 이를 통해 문서의 민감도를 시각적으로 표시하고, 정보 보호를 강화할 수 있습니다.

![image](https://github.com/user-attachments/assets/eeb4c8dd-d35c-432d-a87a-33e69aa6005a)

* Add a watermark: 워터마크를 추가할 수 있는 옵션입니다. 이 옵션을 활성화하면, 문서에 워터마크를 추가하여 문서가 기밀 정보임을 명확히 표시할 수 있습니다.
* Add a header: 헤더를 추가할 수 있는 옵션입니다. 이 옵션을 활성화하면, 문서 상단에 사용자 정의 텍스트를 추가할 수 있습니다.
* Add a footer: 푸터를 추가할 수 있는 옵션입니다. 이 옵션을 활성화하면, 문서 하단에 사용자 정의 텍스트를 추가할 수 있습니다.

4. Container SL 설정하기 

![image](https://github.com/user-attachments/assets/eb47ed55-3d84-480a-9276-5f920d8de125)

![image](https://github.com/user-attachments/assets/91f8c649-bde5-463e-b314-507e0f6833b5)

5. 설정완료
   
![image](https://github.com/user-attachments/assets/7e54f715-8336-49ea-8971-5936f0528fb6)

--------------------------------

### Confidential-Internal SL 설정하기 

1. 설정하기
![image](https://github.com/user-attachments/assets/0e71545d-159a-423c-98cd-3aa124e8a8ea)

![image](https://github.com/user-attachments/assets/e0ccd34a-e678-4a26-86e7-e46bb1dbab07)

2. Item (Access control): Confidential-Internal Label 설정하기- Internal only이기때문에, ‘add all users and groups in your organization’ 추가 

![image](https://github.com/user-attachments/assets/3c0473cc-a095-4524-a01f-cf9d35fc7a4d)

### Access control
![image](https://github.com/user-attachments/assets/a44f533c-9c5d-4ee9-a881-7abb5eff9625)

### Content Marking 
![image](https://github.com/user-attachments/assets/873d551f-3d18-40bb-8399-6826d83c78f3)

3. Container LS (Group & Sites) 설정하기

![image](https://github.com/user-attachments/assets/c65c573f-86f3-47b8-82da-21370fd3c55f)

![image](https://github.com/user-attachments/assets/eed7ec34-2e52-4d68-a3a2-46049116eb0d)

![image](https://github.com/user-attachments/assets/ed0a9e6f-0c66-402c-997d-9b7482d06810)

4. 설정 완료

![image](https://github.com/user-attachments/assets/3cbb1702-bbc6-4afe-b81c-258ef8b104d5)

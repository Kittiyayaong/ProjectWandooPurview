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

![Uploading 스크린샷 2025-06-29 오전 9.44.05.png…]()

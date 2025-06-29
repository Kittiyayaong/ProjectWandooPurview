# Purview Module 03 - Insider Risk Management

## Lab 2.Adaptive Protection

### Adaptive Protection이란?
Adaptive Protection = IRM + DLP + Conditional Access 통합 자동 대응
| 구성 요소                             | 역할                      |
| --------------------------------- | ----------------------- |
| **Insider Risk Management (IRM)** | 사용자 위험도 (Risk Level) 평가 |
| **Data Loss Prevention (DLP)**    | 민감정보 보호 정책 설정           |
| **Conditional Access (CA)**       | 위험도에 따른 접근 제어           |

➔ Adaptive Protection은 IRM에서 Elevated/High Risk로 평가된 사용자의 DLP enforcement level을 자동으로 Block, Encrypt, Restrict로 강화.

### 📌 **시나리오**
이번 Lab은 Module 03 (IRM) 에서 탐지된 Risk score 결과를 Adaptive Protection으로 Enforcement 강화에 연계하는 시나리오입니다.
1. **Confidential – Wandoo 라벨**이 적용된 문서를
   - 외부 메일 전송 시 **Risk alert 생성 (IRM)**
2. 동일 사용자가 **반복적으로 위반**하거나 Risk score가 Elevated 이상으로 상승 시
   - Adaptive Protection이 DLP Enforcement level을 **자동으로 차단(Block)으로 강화**

## [Step 1] Policy Name & Description
1. Purview console > Solutions > Insider Risk Management > Adaptive Protection
2. Setup: Quick Setup으로 진행
| 옵션               | 설명                                                                                                                                                                             | 추천 시나리오                                             |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------- |
| **Quick setup**  | Microsoft 권장 기본 설정으로 Adaptive Protection 활성화<br>✅ 전사 사용자 대상으로 IRM Policy 생성<br>✅ Built-in risk level 설정<br>✅ DLP policy (Audit 모드) 생성<br>✅ Conditional Access (Report-only) 생성 | ✔️ **PoC, Demo, Lab 환경**<br>빠른 테스트 용도               |
| **Custom setup** | 조직 환경, 정책, 사용자 그룹에 맞춘 세부 설정 가능                                                                                                                                                 | ✔️ **실제 운영 환경**<br>보호 대상, DLP 정책, CA 정책을 맞춤 구성 필요 시 |


3. Name: Wandoo – Confidential External Email Adaptive Protection
4. Description: Blocks external email for Elevated risk users detected by IRM.

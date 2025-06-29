# Purview Module 03 - Insider Risk Management

## Lab 2.Adaptive Protection

**Insider Risk Management (IRM)** 에서 탐지된 **Risk score를 기반**으로,  
Microsoft Purview DLP 정책의 **Enforcement level을 자동 조정**하여  
민감정보 유출 방지를 **즉각적이고 동적으로 강화**한다.

### 📌 **시나리오**

1. **Confidential – Wandoo 라벨**이 적용된 문서를
   - 외부 메일 전송 시 **Risk alert 생성 (IRM)**
2. 동일 사용자가 **반복적으로 위반**하거나 Risk score가 Elevated 이상으로 상승 시
   - Adaptive Protection이 DLP Enforcement level을 **자동으로 차단(Block)으로 강화**

## [Step 1] Policy Name & Description
1. Purview console > Solutions > Insider Risk Management > Adaptive Protection
2. 

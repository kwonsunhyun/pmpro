---
description: 카카오페이 간편결제 설정 방법을 확인합니다.
---

# ⌨ 카카오페이 설정

## 일반**결제**

{% tabs %}
{% tab title="테스트 결제" %}
### 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(<mark style="color:red;">**일반결제 및 정기결제**</mark>) → PG사 \[간편결제]카카오페이 선택 → 테스트모드 \[ON] → 가맹점코드(CID)에 **TC0ONETIME** 입력 > \[전체 저장] 클릭



![](<../../../.gitbook/assets/image (12) (1) (1) (1).png>)
{% endtab %}

{% tab title="실 결제" %}
### **실** 환경 구성방법

**테스트모드 OFF** 처리 이후 카드사 심사 완료 후 카카오페이에서 발급받은 실상점 정보를 설정합니다.



![](<../../../.gitbook/assets/image (6) (1) (1).png>)
{% endtab %}
{% endtabs %}

## 정기결제

### 카카오페이의 정기결제는 결제창 방식만 지원합니다.

{% tabs %}
{% tab title="결제창 방식" %}
### 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(<mark style="color:red;">**일반결제 및 정기결제**</mark>) → PG사 \[간편결제]카카오페이 선택 → 테스트모드 \[ON] → 가맹점코드(CID)에 '**TCSUBSCRIP**' 입력 > \[전체 저장] 클릭

![](<../../../.gitbook/assets/image (7) (1) (1).png>)

### 실  환경 구성방법

**테스트모드 OFF** 처리 이후 카드사 심사 완료 후 카카오페이에서 발급받은 실상점 정보를 설정합니다.
{% endtab %}
{% endtabs %}


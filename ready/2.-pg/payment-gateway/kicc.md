---
description: KICC 설정 방법을 안내합니다.
---

# ⌨ KICC 설정

## 인증**결제**

{% tabs %}
{% tab title="테스트 결제" %}
### 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/) → 시스템설정 → PG설정(**일반결제 및 정기결제**) → PG사 KICC-한국정보통신 선택 → <mark style="color:red;">**테스트모드 \[ON]**</mark> → \[전체 저장] 클릭


{% endtab %}

{% tab title="실 결제" %}
### **실** 환경 구성방법

카드사 심사 완료 후 KICC 에서 발급받은 실 상점 정보를 <mark style="color:red;">**테스트모드 OFF**</mark> 이후 설정합니다.



![실 환경 설정 예시](<../../../.gitbook/assets/image (5) (1) (1).png>)
{% endtab %}
{% endtabs %}

## 비 인증 결제

{% tabs %}
{% tab title="결제창 방식" %}
### 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(**일반결제 및 정기결제**) → PG사 KICC-한국정보통신 선택 → <mark style="color:red;">**테스트모드 \[ON]**</mark> → \[전체 저장] 클릭



![](<../../../.gitbook/assets/image (28) (1) (1) (1).png>)

### **실** 환경 구성방법

카드사 심사 완료 후 KICC 에서 발급받은 실상점 정보를 <mark style="color:red;">**테스트모드 OFF**</mark> 이후 설정합니다.

![실 환경 설정 예시](<../../../.gitbook/assets/image (20) (1) (1) (1) (1) (1).png>)
{% endtab %}

{% tab title="API 방식" %}
#### 아임포트를 통한 KICC API 비 인증 결제 방식은 지원되지 않습니다.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**참고 사항**&#x20;

KICC(한국정보통신)의 테스트 모드에서는 실제 출금 되지 않습니다.
{% endhint %}

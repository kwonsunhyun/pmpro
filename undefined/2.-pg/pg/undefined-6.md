---
description: 세틀뱅크 설정방법을 안내합니다.
---

# ⌨ 세틀뱅크 설정

## 인증결제

{% tabs %}
{% tab title="테스트 결제" %}
### 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(**일반결제 및 정기결제**) → PG사 세틀뱅크 선택 → <mark style="color:red;">**테스트모드 \[ON]**</mark> → \[전체 저장] 클릭



![테스트 환경 설정예시](<../../../.gitbook/assets/image (20).png>)
{% endtab %}

{% tab title="실 결제" %}
### **실** 환경 구성방법

카드사 심사 완료 후 세틀뱅크에서 발급받은 실상점 정보를 ** **<mark style="color:red;">**테스트모드 OFF**</mark> 처리 이후 설정합니다.



![실 계정 설정 예시](<../../../.gitbook/assets/image (8).png>)
{% endtab %}
{% endtabs %}

## 비 인증 결제&#x20;

{% tabs %}
{% tab title="결제창 방식" %}
#### **세틀뱅크의 정기결제는 **<mark style="color:red;">**REST API 방식**</mark>**만 지원합니다.**
{% endtab %}

{% tab title="API 방식" %}
### 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(<mark style="color:red;">**정기결제 및 키인결제**</mark>) → PG사 세틀뱅크 선택 → \[**카드사 심사 전 개발용 계정 설정**] 클릭 → \[저장] 클릭



![테스트 환경 설정 예시](<../../../.gitbook/assets/image (11).png>)

### 가상계좌 연동 방법

아래 링크를 참조하여 가상계좌 발급 및 취소 API 를 연동합니다.

{% content-ref url="../../../api/api-9/" %}
[api-9](../../../api/api-9/)
{% endcontent-ref %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
#### **세틀뱅크는 가상계좌 발급을 API방식으로 지원합니다.**
{% endhint %}

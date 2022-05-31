---
description: JTNET PG사 설정 방법을 확인합니다.
---

# ⌨ JTNET 설정

## 인증결제

{% tabs %}
{% tab title="테스트 결제" %}
### 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(<mark style="color:red;">**일반결제 및 정기결제**</mark>) → PG사 JTNet(tPay) 선택 → 테스트모드 \[ON] → \[전체 저장] 클릭

{% hint style="info" %}
**테스트MID 정보**

* MID : tpaytest0m&#x20;
* Secret 키 : VXFVMIZGqUJx29I/k52vMM8XG4hizkNfiapAkHHFxq0RwFzPit55D3J3sAeFSrLuOnLNVCIsXXkcBfYK1wv8kQ==&#x20;
* 취소비밀번호 : 123456
{% endhint %}



![](<../../../.gitbook/assets/image (20).png>)
{% endtab %}

{% tab title="실결제" %}
### **실** 환경 구성방법

카드사 심사 완료 후 JTNet에서 발급받은 실상점 정보를 **테스트모드 **<mark style="color:red;">**OFF**</mark> 처리 이후 설정합니다.



![](<../../../.gitbook/assets/image (16).png>)
{% endtab %}
{% endtabs %}

## 비 인증 결제&#x20;

{% tabs %}
{% tab title="결제창 방식" %}

{% endtab %}

{% tab title="API 방식" %}


[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(정기결제 및 키인결제) → PG사 JTNet(tPay) 선택 → 테스트모드 \[OFF] → 키인결제용 상점정보 입력 후 \[전체 저장] 클릭
{% endtab %}
{% endtabs %}

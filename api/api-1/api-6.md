---
description: 인증 결제시 결제금액을 사전등록 하여 금액 위변조로 인한 결제사고를 예방합니다.
---

# ⌨ 결제금액 사전등록 API

### 인증결제를 진행할 때 결제금액 위변조 시 결제진행자체를 block 하기 위해 결제예정금액을 사전등록하는 기능

{% swagger method="post" path="/payments/prepare" baseUrl="https://api.iamport.kr" summary="결제 금액을 사전 등록합니다." %}
{% swagger-description %}
사전등록된 가맹점 주문번호(merchant_uid)에 대해, IMP.request_pay()에 전달된 merchant_uid가 일치하는 주문의 결제금액이 다른 경우 PG사 결제창 호출이 중단됩니다
{% endswagger-description %}

{% swagger-parameter in="body" name="merchant_uid" type="String" required="true" %}
<mark style="color:red;">

**가맹점 주문번호**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="double" required="true" %}
<mark style="color:red;">

**결제 예정금액**

</mark>

 
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
{% tabs %}
{% tab title="PaymentPrepareResponse" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



<mark style="color:red;">**`response (PaymentPrepareAnnotation, optional)`**</mark>
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="PaymentPrepareAnnotation" %}
**merchant\_uid **<mark style="color:red;">**`*`**</mark>**` `**<mark style="color:green;">**`string`**</mark>

**가맹점 주문번호 **<mark style="color:green;">****</mark>&#x20;

<mark style="color:green;">****</mark>

**`amount`**<mark style="color:red;">**`*`**</mark><mark style="color:orange;">**`number`**</mark><mark style="color:orange;">** **</mark><mark style="color:orange;">****</mark>&#x20;

**`결제 예정 금액`**
{% endtab %}
{% endtabs %}
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="인증 Token이 전달되지 않았거나 유효하지 않은 경우" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

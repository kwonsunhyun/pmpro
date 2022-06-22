---
description: POST /payments/prepare 로 이미 등록된 결제사전정보에 대해 금액을 수정하는 기능입니다.
---

# ⌨ 결제금액 단건 수정 API

### [**결제금액 사전등록 API**](api-6.md) 로  등록된 금액을 수정합니다.

{% swagger method="put" path="/payments/prepare" baseUrl="https://api.iamport.kr" summary="사전등록한 결제 금액을 단건 수정 합니다." %}
{% swagger-description %}

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

{% swagger-response status="404: Not Found" description="요청된 merchant_uid 로 등록된 결제사전정보를 찾을 수 없는 경우" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

<details>

<summary>Response Model Schema</summary>

```
{
  "code": 0,
  "message": "string",
  "response": {
    "merchant_uid": "string",
    "amount": 0
  }
}
```

</details>

{% hint style="success" %}
**Swagger Test Link**

****[**https://api.iamport.kr/#!/payments.validation/editPreparePayment**](https://api.iamport.kr/#!/payments.validation/editPreparePayment)****
{% endhint %}

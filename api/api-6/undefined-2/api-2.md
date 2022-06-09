---
description: 네이버페이 현금영수증 발급가능 금액 조회 API
---

# ⌨ 현금영수증 발급 가용액 조회 API

### 네이버페이 결제형 현금영수증 발급가능 금액 조회 API

{% swagger method="get" path="/payments/{imp_uid}/naver/cash-amount" baseUrl="https://api.iamport.kr" summary="현금영수증 발급가능 금액 조회" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="imp_uid" type="String" required="true" %}
<mark style="color:red;">

**아임포트 거래번호**

</mark>
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
{% tabs %}
{% tab title="NaverCashAmountResponse" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`response`` `**<mark style="color:red;">**`(NaverCashAmountAnnotation, optional)`**</mark>
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="NaverCashAmountAnnotation" %}
**`amount_total`` `**<mark style="color:purple;">**`integer`**</mark>

**`현금영수증 발급가능 총액` **<mark style="color:red;">****</mark>&#x20;

&#x20;****&#x20;

**`amount_by_npoint`** <mark style="color:purple;">**`integer`**</mark>&#x20;

**`현금영수증 발급가능 총액 중 Npoint 에 의한 금액`**



**`amount_by_primary`** <mark style="color:purple;">**`integer`**</mark>

**`현금영수증 발급가능 총액 중 메인 결제수단(신용카드, 계좌이체 등)에 의한 금액`**



**`amount_supply`** <mark style="color:purple;">**`integer`**</mark>

**`현금영수증 발급가능 총액 중 공급가액`**



**`amount_vat`** <mark style="color:purple;">**`integer`**</mark>

**`현금영수증 발급가능 총액 중 부가세`**
{% endtab %}
{% endtabs %}
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="네이버페이 결제형 거래가 아닌 건에 대해 요청하는 경우" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="인증 Token이 전달되지 않았거나 유효하지 않은 경우" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="네이버페이 현금영수증 발급가능 금액 조회시 네이버응답이 올바르지 않은 경우" %}
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
    "amount_total": 0,
    "amount_by_npoint": 0,
    "amount_by_primary": 0,
    "amount_supply": 0,
    "amount_vat": 0
  }
}
```

</details>

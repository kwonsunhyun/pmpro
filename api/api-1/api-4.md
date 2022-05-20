---
description: 복합결제거래 상세정보를 조회합니다.
---

# ⌨ 결제 상세내역 조회 API

### 복합결제거래 상세정보를 조회합니다.

{% swagger method="get" path="/payments/{imp_uid}/balance" baseUrl="https://api.iamport.kr" summary="복수의 결제수단으로 거래가 발생된 거래의 상세 금액정보를 확인합니다." %}
{% swagger-description %}
현재 PAYCO 결제수단에 한해 제공되고 있습니다
{% endswagger-description %}

{% swagger-parameter in="path" name="imp_uid" type="String" required="true" %}
<mark style="color:red;">

**차이포트 거래번호**

</mark>
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
{% tabs %}
{% tab title="PaymentBalanceResponse" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



&#x20;**`response`` `**<mark style="color:red;">**`(PaymentBalanceResponseAnnotation, optional)`**</mark>
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="PaymentBalanceResponseAnnotation" %}
**`amount`` `**<mark style="color:purple;">**`Integer`**</mark>

**`총 결제금액`**

&#x20;****&#x20;

**`cash_receipt`` `**<mark style="color:red;">**`(PaymentBalanceAnnotation):`**</mark>&#x20;

**`현금영수증 발급된 금액 상세`**



**`primary`` `**<mark style="color:red;">**`(PaymentBalanceAnnotation):`**</mark>&#x20;

**`1차 결제수단`**(신용카드, 계좌이체, 가상계좌, 휴대폰소액결제) 금액 상세



**`secondary`` `**<mark style="color:red;">**`(PaymentBalanceAnnotation):`**</mark>&#x20;

**`2차 결제수단`**(PG사포인트, 카드사포인트) 금액 상세



**`discount`` `**<mark style="color:red;">**`(PaymentBalanceAnnotation):`**</mark>&#x20;

**`PG사/카드사 자체 할인 금액 상세`**



**`histories`` `**<mark style="color:red;">**`(Array[PaymentBalanceBaseAnnotation], optional)`**</mark>&#x20;

**`PaymentBalance 이력` **<mark style="color:red;">****</mark>&#x20;
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="PaymentBalanceAnnotation" %}
**`tax_free`` `**<mark style="color:purple;">**`Integer`**</mark>

**`면세 공급가액`** (환불시 마이너스 차감된 최종 금액 반환)



**`supply`` `**<mark style="color:purple;">**`Integer`**</mark>

**`과세 공급가액`** (환불시 마이너스 차감된 최종 금액 반환)



**`vat`** <mark style="color:purple;">**`Integer`**</mark>

**`부가세액`** (환불시 마이너스 차감된 최종 금액 반환)



**`service`` `**<mark style="color:purple;">**`Integer`**</mark>

**`봉사료`** (환불시 마이너스 차감된 최종 금액 반환)
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="PaymentBalanceBaseAnnotation" %}
**`cash_receipt` **<mark style="color:red;">**(PaymentBalanceAnnotation):**</mark>&#x20;

**`현금영수증 발급된 금액 상세`**

&#x20;****&#x20;

**`primary`` `**<mark style="color:red;">**`(PaymentBalanceAnnotation)`**</mark>&#x20;

**`1차 결제수단`**(신용카드, 계좌이체, 가상계좌, 휴대폰소액결제) 금액 상세



**`secondary`` `**<mark style="color:red;">**`(PaymentBalanceAnnotation):`**</mark>

**`2차 결제수단`**(PG사포인트, 카드사포인트) 금액 상세



**`discount`` `**<mark style="color:red;">**`(PaymentBalanceAnnotation)`**</mark>

**`PG사/카드사 자체 할인 금액 상세`**



**`created  *`` `**<mark style="color:purple;">**`integer`**</mark> <mark style="color:purple;"></mark><mark style="color:purple;"></mark>&#x20;

**`Balance정보가 등록된 시각 UNIX timestamp`**
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

{% swagger-response status="404: Not Found" description="유효하지 않은 imp_uid" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

### Response Model Schema

<details>

<summary>HTTP status 200</summary>

```json
{
  "code": 0,
  "message": "string",
  "response": {
    "amount": 0,
    "cash_receipt": {
      "tax_free": 0,
      "supply": 0,
      "vat": 0,
      "service": 0
    },
    "primary": {
      "tax_free": 0,
      "supply": 0,
      "vat": 0,
      "service": 0
    },
    "secondary": {
      "tax_free": 0,
      "supply": 0,
      "vat": 0,
      "service": 0
    },
    "discount": {
      "tax_free": 0,
      "supply": 0,
      "vat": 0,
      "service": 0
    },
    "histories": [
      {
        "cash_receipt": {
          "tax_free": 0,
          "supply": 0,
          "vat": 0,
          "service": 0
        },
        "primary": {
          "tax_free": 0,
          "supply": 0,
          "vat": 0,
          "service": 0
        },
        "secondary": {
          "tax_free": 0,
          "supply": 0,
          "vat": 0,
          "service": 0
        },
        "discount": {
          "tax_free": 0,
          "supply": 0,
          "vat": 0,
          "service": 0
        },
        "created": 0
      }
    ]
  }
}
```

</details>

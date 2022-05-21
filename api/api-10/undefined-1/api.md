---
description: 편의점 결제를 위한 수납번호를 발급합니다.
---

# ⌨ 수납번호 발급 API

### 편의점결제 수납번호(barcode)를 발급 또는 등록합니다.

{% swagger method="post" path="/cvs" baseUrl="https://api.iamport.kr" summary="편의점결제 수납번호(barcode) 발급" %}
{% swagger-description %}
편의점결제를 위한 수납번호(barcode)를 사전 발급 또는 등록합니다. 고객은 발급 또는 등록된 수납번호(barcode)에 해당되는 바코드 이미지 또는 수납번호를 편의점 방문시 제시함으로써 현장 결제가 이뤄지게 됩니다.
{% endswagger-description %}

{% swagger-parameter in="body" name="merchant_uid" type="String(40)" required="true" %}
<mark style="color:red;">

**주문번호**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="double" required="true" %}
<mark style="color:red;">

**결제금액**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="barcode" type="String" %}
**바코드**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expired_at" type="integer" %}
**편의점 수납가능한 결제기한**

Unix Timestamp
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="String(40)" %}
**제품명**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_name" type="String(16)" %}
**주문자명**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_email" type="String(64)" %}
**주문자 E-mail주소**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_tel" type="String(16)" %}
**주문자 전화번호**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_addr" type="String(128)" %}
**주문자 주소**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_postcode" type="String(8)" %}
**주문자 우편번호**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pg" type="String" %}
**PG구분코드**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="confirm_url" type="String" %}
**수납가능여부 체크 URL**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notice_url" type="String" %}
**편의점결제 수납성공 시 통지받을 URL**

선언되지 않으면 아임포트 관리자 페이지에 정의된 Notification URL값을 사용
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_data" type="Array" %}
**에코항목**

 
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
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
{% endswagger %}

### **주요 요청 파라미터 상세 설명**

> **barcode  **<mark style="color:green;">**string**</mark>
>
> **`바코드번호`**
>
> 가맹점에서 직접 생성/관리하는 바코드(barcode)번호가 있는 경우 갤럭시아컴즈로부터 신규 수납번호(barcode)를 발급요청하지 않고 가맹점에서 관리하는 바코드(barcode)번호를 등록하여 수납번호로 활용할 수 있다.

> **expired\_at  **<mark style="color:purple;">**integer**</mark>
>
> **`편의점 수납가능한 결제기한` **<mark style="color:purple;">****</mark>&#x20;
>
> 정의하지 않으면 갤럭시아컴즈와 계약시 협의한 기본값이 적용됨

> **`pg`` `**<mark style="color:purple;">**``**</mark>**` `**<mark style="color:green;">**`String`**</mark>
>
> **`PG사 구분자` **<mark style="color:green;">****</mark>&#x20;
>
> 갤럭시아컴즈 상점아이디를 2개 이상 동시에 사용하시려는 경우 설정하시면 됩니다.&#x20;
>
> **galaxia.{상점아이디}** 형태로 지정

> **`confirm_url`**<mark style="color:green;">**`string`**</mark>
>
> 고객이 편의점결제 수납시도 시 수납가능여부를 체크하기 위한 URL. 설정하지 않은 결제에 대해서는 항상 수납가능으로 간주하고 수납성공진행 됨.&#x20;
>
> 설정된 결제에 대해서는 해당 URL로 아래와 같은 형식의 데이터가 Webhook(HTTP POST)으로 전송됩니다.
>
> **`200응답 == 수납가능 / 그 외응답 == 수납불가 처리` **<mark style="color:green;">****</mark>&#x20;
>
> <mark style="color:green;">****</mark>
>
> {% code title="Webhook Body" %}
> ```json
> {
>     event : 'Galaxia.Cvs.Confirm',
>     imp_uid : 'imp_123412341234',
>     merchant_uid : 'asdfasdfasdf',
>     status : 'ready',
>     extra : {
>         barcode : '11222222',
>         payType : 'card' //card or cash
>     }
> }
> ```
> {% endcode %}

<details>

<summary>Response Model Schema</summary>

```json
{
  "code": 0,
  "message": "string",
  "response": {
    "imp_uid": "string",
    "merchant_uid": "string",
    "pay_method": "string",
    "channel": "pc",
    "pg_provider": "string",
    "emb_pg_provider": "string",
    "pg_tid": "string",
    "pg_id": "string",
    "escrow": true,
    "apply_num": "string",
    "bank_code": "string",
    "bank_name": "string",
    "card_code": "string",
    "card_name": "string",
    "card_quota": 0,
    "card_number": "string",
    "card_type": "null",
    "vbank_code": "string",
    "vbank_name": "string",
    "vbank_num": "string",
    "vbank_holder": "string",
    "vbank_date": 0,
    "vbank_issued_at": 0,
    "name": "string",
    "amount": 0,
    "cancel_amount": 0,
    "currency": "string",
    "buyer_name": "string",
    "buyer_email": "string",
    "buyer_tel": "string",
    "buyer_addr": "string",
    "buyer_postcode": "string",
    "custom_data": "string",
    "user_agent": "string",
    "status": "ready",
    "started_at": 0,
    "paid_at": 0,
    "failed_at": 0,
    "cancelled_at": 0,
    "fail_reason": "string",
    "cancel_reason": "string",
    "receipt_url": "string",
    "cancel_history": [
      {
        "pg_tid": "string",
        "amount": 0,
        "cancelled_at": 0,
        "reason": "string",
        "receipt_url": "string"
      }
    ],
    "cancel_receipt_urls": [
      "string"
    ],
    "cash_receipt_issued": true,
    "customer_uid": "string",
    "customer_uid_usage": "issue"
  }
}
```

</details>

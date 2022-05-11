---
description: 가상계좌번호를 발급하여 고객이 입금할수 있도록 합니다.
---

# ⌨ 가상계좌 발급 API

### 가상계좌번호를 발급할수 있습니다.

해당 API 는 아래 PG사를 이용하는 경우에만 사용 가능합니다.

* 세틀뱅크
* 나이스페이먼츠
* KG이니시스

{% swagger method="post" path="/vbanks" baseUrl="https://api.iamport.kr" summary="가상계좌 번호를 발급합니다." %}
{% swagger-description %}
희망하시는 은행, 예금주명으로 입금이 가능한 가상계좌를 생성할 수 있습니다.(별도로 PG계약 필요)


{% endswagger-description %}

{% swagger-parameter in="body" name="merchant_uid" type="String(40)" required="true" %}
<mark style="color:red;">

**주문번호**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="Double" required="true" %}
<mark style="color:red;">

**발급금액**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="vbank_code" type="String" required="true" %}
<mark style="color:red;">

**은행구분코드**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="vbank_due" type="Integer" required="true" %}
<mark style="color:red;">**가상계좌 입금기한**</mark>

**UNIX TIMESTAMP **<mark style="color:red;">****</mark>&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="vbank_holder" type="String(16)" required="true" %}
<mark style="color:red;">

**가상계좌 예금주명**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="String(40)" %}
**주문명**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_name" type="String(16)" %}
**주문자명**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_email" type="String(64)" %}
**주문자 E-mail 주소**
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
**PG사 구분코드**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notice_url" type="String" %}
**입금통보 URL**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_data" type="Array" %}
**에코항목**
{% endswagger-parameter %}

{% swagger-parameter in="query" name="pg_api_key" type="String" %}
**API Key**

**(이니시스 전용)**
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}

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

> **`vbank_code`` `**<mark style="color:red;">**`*`**</mark>**` `**<mark style="color:green;">**`String`**</mark>
>
> **은행구분코드 **<mark style="color:green;">****</mark>&#x20;
>
> [**은행코드표**](../../tip/pg.md) 참조

> **`pg`    **<mark style="color:red;">**\***</mark>**    **<mark style="color:green;">**string**</mark>
>
> **pg 구분코드**
>
> 관리자콘솔 API 방식 비인증 PG설정이 2개 이상인 경우 필수적으로 기재해야 하는 항목입니다.
>
> 동일 PG사에 <mark style="color:red;">**두개의 MID**</mark> 를 설정한 경우 아래 양식으로 기재 합니다. ****&#x20;
>
> **{PG사}.{PG상점아이디}**
>
> 지정하지 않거나 유효하지 않은 값이 전달되면 기본PG설정된 값을 이용해 결제하게 됩니다.
>
> * 나이스페이먼츠, JTNet 2가지 PG설정이 되어있다면, pg 파라메터로 **nice** 또는 **jtnet**로 구분 가능
> * 나이스페이먼츠로부터 2개 이상의 상점아이디를 발급받았다면, **nice.MID1** 또는 **nice.MID2**로 구분 가능

> **`notice_url``  `**<mark style="color:green;">**`String`**</mark>
>
> **입금통보 URL **<mark style="color:green;">****</mark>&#x20;
>
> 가상계좌 입금시 입금통지받을 URL 선언되지 않으면 아임포트 관리자 페이지에 정의된 Notification URL값을 사용

> **`custom_data`**<mark style="color:blue;">**`json`**</mark>
>
> **에코항목** <mark style="color:blue;"></mark>&#x20;
>
> 결제정보와 함께 저장할 custom\_data. 객체로 전달되는 경우 JSON 문자열로 저장

> **`pg_api_key`**<mark style="color:green;">**`String`**</mark>
>
> 이니시스의 가맹점 콘솔에서 확인하셔야 하는 API Key 값으로 가상계좌 발급 및 말소 신청에 사용됩니다. 누락하거나 잘못된 키 입력 시 hashData 불일치 오류가 발생합니다.&#x20;
>
> (**이니시스 전용이며, 이니시스의 경우 필수값 Query parameter임**)

### Respose Model Schema

<details>

<summary>HTTP status 200</summary>

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


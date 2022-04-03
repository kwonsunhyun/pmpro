---
description: 저장된 빌링키(customer_uid)를 이용하여 결제를 요청할 수 있는 API 명세를 기술합니다.
---

# ⌨ 비 인증 결제(빌링키) API

### 저장된 빌링키(customer\_uid)로 결제를 요청 할수 있습니다.

{% swagger method="post" path="/subscribe/payments/again" baseUrl="https://api.iamport.kr" summary="customer_uid 로 결제를 요청합니다." %}
{% swagger-description %}
빌링키 발급 API 또는 PG사 빌링키 발급 결제창에서 설정한 

**customer_uid**

 로 비 인증 결제를 요청할 수 있습니다.
{% endswagger-description %}

{% swagger-parameter in="body" name="customer_uid" type="String" required="true" %}
실 빌링키와 1:1로 매칭될 고유번호
{% endswagger-parameter %}

{% swagger-parameter in="body" name="merchant_uid" type="String" required="true" %}
주문번호
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="String" %}
결제 통화코드
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="integer" required="true" %}
결제금액
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tax_free" type="integer" %}
면세금액
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="String" required="true" %}
제품명
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_name" type="String" %}
주문자명
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_email" type="String" %}
주문자 E-mail주소
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_tel" type="String" %}
주문자 전화번호
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_addr" type="String" %}
주문자 주소
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_postcode" type="String" %}
주문자 우편번호
{% endswagger-parameter %}

{% swagger-parameter in="body" name="card_quota" type="integer" %}
카드 할부개월수
{% endswagger-parameter %}

{% swagger-parameter in="body" name="interest_free_by_merchant" type="boolean" %}
가맹점부담 무이자 할부여부
{% endswagger-parameter %}

{% swagger-parameter in="body" name="use_card_point" type="boolean" %}
카드포인트 사용여부
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_data" type="String" %}
에코항목
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notice_url" type="String" %}
결제성공 시 통지될 웹훅 URL
{% endswagger-parameter %}

{% swagger-parameter in="body" name="browser_ip" type="String" %}
구매자 브라우져(PC)의 IP
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="결제성공" %}
{% tabs %}
{% tab title="First Tab" %}
> **code  **<mark style="color:red;">**\***</mark>**    **<mark style="color:purple;">**integer**</mark>
>
> **응답코드**
>
> 0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



> **message **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>
>
> **응답메세지**
>
> code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다
{% endtab %}

{% tab title="Model Schema" %}
{% code title="json" %}
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

son
```
{% endcode %}
{% endtab %}
{% endtabs %}

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

---
description: 모든 결제내역을 취소할 수 있는 API 를 안내합니다.
---

# ⌨ 결제취소 API

### **결제수단 및 PG사와 상관없이 취소 및 부분취소가 가능합니다.**

{% swagger method="post" path="/payments/cancel" baseUrl="https://api.iamport.kr" summary="승인된 결제를 취소합니다." %}
{% swagger-description %}
신용카드/실시간계좌이체/휴대폰 소액결제의 경우 즉시 취소처리가 이뤄지게 되며 가상계좌의 경우는 환불받으실 계좌정보를 같이 전달해주시면 환불정보가 PG사에 등록되어 익영업일에 처리됩니다.

**(가상계좌 환불관련 특약계약 필요)**
{% endswagger-description %}

{% swagger-parameter in="body" name="imp_uid" type="String(32)" required="true" %}
<mark style="color:red;">

**차이포트 거래고유번호**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="merchant_uid" type="String(40)" %}
**주문번호 (imp_uid 누락시 필수)**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="Double" required="false" %}
취소 요청금액 

<mark style="color:red;">



</mark>

 (

**누락시 전액취소**

) 

<mark style="color:purple;">

****

</mark>

 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tax_free" type="Double" %}
취소요청금액 중 면세금액 (

**누락되면 0원처리**

)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="checksum" type="Double" %}
현재시점의 취소 가능한 잔액.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="reason" type="String(256)" %}
**취소사유**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="refund_holder" type="String(16)" %}
**환불계좌 예금주**

 (

**가상계좌**

 취소시 필수)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="refund_bank" type="String(4)" %}
환불계좌 은행코드 (하단 은행코드표 참조, 

**가상계좌 취소시**

 필수)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="refund_account" type="String(16)" %}
환불계좌 계좌번호 (

**가상계좌**

 취소시 필수)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="refund_tel" type="String(16)" %}
환불계좌 예금주 연락처(

**가상계좌**

 취소,

<mark style="color:red;">

**스마트로 PG사 인경우 필수**

</mark>

 )
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="취소 성공" %}
{% tabs %}
{% tab title="PaymentResponse" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`response`** <mark style="color:red;">**(PagedPaymentAnnotation, optional)**</mark>
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="PaymentAnnotation" %}
**`imp_uid`** <mark style="color:red;">\*</mark> <mark style="color:green;">**string(32)**</mark>

**아임포트 결제 고유 UID**

****

**`merchant_uid`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string(40)**</mark>

**주문번호**

****

**`pay_method`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string(20)**</mark>

**결제수단 구분코드**

****

**`channel`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string(10)**</mark>

**결제환경 구분코드**

&#x20;\['pc', 'mobile', 'api']



**`pg_provider`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string(16)**</mark>

**PG사 구분코드**

***

**`emb_pg_provider`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string(16)**</mark>

**허브형결제 PG사 구분코드**



**`pg_tid`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string(80)**</mark>

**pg사 거래번호**

****

**`pg_id`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string(80)**</mark>

**PG사 MID**

****

**`escrow`  ** <mark style="color:orange;">**boolean**</mark>

**에스크로 결제여부**

****

**`apply_num`**  ** **<mark style="color:green;">**string(20)**</mark>

**신용카드 승인번호**

****

**`bank_code`**  <mark style="color:red;">****</mark>** **<mark style="color:green;">**string(4)**</mark>

**은행 표준코드(링크보기)**

****

**`bank_name`**  <mark style="color:red;">****</mark>** **<mark style="color:green;">**string(20)**</mark>

**은행 명칭**

***

**`card_code`**  <mark style="color:red;">****</mark>** **<mark style="color:green;">**string(3)**</mark>

**카드사 코드번호(금융결제원 표준코드번호 :** [<mark style="color:red;">**링크**</mark>](https://chaifinance.notion.site/53589280bbc94fab938d93257d452216?v=eb405baf52134b3f90d438e3bf763630) )



**`card_name`**  <mark style="color:green;">**string(20)**</mark>

**카드사명**

****

**`card_quota`** ** **<mark style="color:purple;">**integer**</mark>

**할부개월 수(0이면 일시불)**

****

**`card_number`** <mark style="color:green;">**string(20)**</mark>

**마스킹 카드번호**

***

**`card_type`**  <mark style="color:green;">**string(2)**</mark>

**카드 구분코드**



**`vbank_code`** ** **<mark style="color:green;">**string(4)**</mark>

**가상계좌 은행 표준코드(하단이미지 참고)**

***

**`vbank_name`** ** **<mark style="color:green;">**string(20)**</mark>

**입금받을 가상계좌 은행명**

****

**`vbank_holder`**  <mark style="color:green;">**string(16)**</mark>

**입금받을 가상계좌 예금주**

****

**`vbank_date`** ** **<mark style="color:green;">**string**</mark>

**입금받을 가상계좌 마감기한 (UNIX timestamp)**

****

**`vbank_issued_at`** ** **<mark style="color:green;">**string**</mark>

**가상계좌 생성 시각 (UNIX timestamp)**

****

**`name`    **<mark style="color:green;">**string(40)**</mark>

**제품명**

****

**`amount`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:purple;">**integer**</mark>

**주문(결제)금액**

****

**`cancel_amount`** ** **<mark style="color:purple;">**integer**</mark>

**결제취소금액**

****

**`currency`    **<mark style="color:green;">**string(3)**</mark>

**통화구분코드**

***

**`buyer_name`    **<mark style="color:green;">**string(16)**</mark>

**주문자명**

****

**`buyer_email`    **<mark style="color:green;">**string(64)**</mark>

**주문자 Email주소**\
****

**`buyer_tel`    **<mark style="color:green;">**string(16)**</mark>

**주문자 전화번호**

****

**`buyer_addr`    **<mark style="color:green;">**string(128)**</mark>

**주문자 주소**

****

**`buyer_postcode`    **<mark style="color:green;">**string(8)**</mark>

**주문자 우편번호**

****

**`custom_data`    **<mark style="color:green;">**string**</mark>

**echo data JSON string으로 전달**

****

**`user_agent`    **<mark style="color:green;">**string(256)**</mark>

**결제를 시작한 단말기의 UserAgent**

****

**`status`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string(20)**</mark>

**결제상태 구분코드**



**`started_at`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**결제시작시점 (UNIX timestamp)**

****

**`paid_at`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**결제완료시점 (UNIX timestamp)**\
****

**`failed_at`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**결제실패시점 (UNIX timestamp)**

****

**`cancelled_at`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**결제취소시점 (UNIX timestamp)**

****

**`fail_reason`** <mark style="color:green;">**string(256)**</mark>

**결제실패 사유**

****

**`cancel_reason`**  <mark style="color:green;">**string(256)**</mark>

**결제취소 사유**

****

**`receipt_url`**  <mark style="color:green;">**string(300)**</mark>

**신용카드 매출전표 확인 URL**

****

**`cash_receipt_issued`  **<mark style="color:orange;">**boolean**</mark>

**현금영수증 자동발급 여부**

****

**`customer_uid`    **<mark style="color:green;">**string(80)**</mark>

**해당 결제처리에 사용된 customer\_uid**

****

**`customer_uid_usage`    **<mark style="color:green;">**string**</mark><mark style="color:green;">**(20)**</mark>

**customer\_uid 사용 구분코드**

\['issue', 'payment', 'payment.scheduled']

****

**`cancel_history` ** <mark style="color:red;">**(Array\[PaymentCancelAnnotation], optional):**</mark>

**`취소/부분취소 내역`**
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="PaymentCancelAnnotation" %}
**cancel\_history array \[]**

**`pg_tid`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**PG사 승인취소번호**

****

**`amount`  **<mark style="color:red;">**\***</mark> <mark style="color:purple;">**integer**</mark>

**취소 금액**

****

**`cancelled_at`  **<mark style="color:red;">**\***</mark> <mark style="color:green;">**string**</mark>

결제취소된 시각 UNIX timestamp



**`reason`** <mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string(256)**</mark>

**결제취소 사유**

****

**`receipt_url`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string(300)**</mark>

**취소에 대한 매출전표 확인 URL. PG사에 따라 제공되지 않는 경우도 있음**
{% endtab %}
{% endtabs %}
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="인증 Token이 전달되지 않았거나 유효하지 않은 경우" %}

{% endswagger-response %}
{% endswagger %}

### **주요 요청 파라미터 상세 설명**

> **`imp_uid`  & `merchant_uid`**
>
> **취소 요청시 두 파라미터중 하나는 필수로 유입되어야 합니다.**

> **`checksum`    **<mark style="color:purple;">**integer**</mark>
>
> **승인 잔액**
>
> API요청자가 기록하고 있는 취소가능 잔액과 아임포트가 기록하고 있는 취소가능 잔액이 일치하는지 사전에 검증하고 검증에 실패하면 트랜잭션을 수행하지 않습니다. null인 경우에는 검증 프로세스를 생략합니다.

> **`amount`  **<mark style="color:green;">****</mark>**  **<mark style="color:red;">**\***</mark>**  **<mark style="color:purple;">**integer**</mark>
>
> **취소금액**
>
> 누락시 전액취소 됩니다.

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

{% hint style="success" %}
**Swagger Test Link**

****[**https://api.iamport.kr/#!/payments/cancelPayment**](https://api.iamport.kr/#!/payments/cancelPayment)****
{% endhint %}

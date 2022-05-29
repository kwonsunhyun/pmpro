---
description: API를 통해 베네피아 포인트(복지포인트)사용 결제요청
---

# ⌨ 포인트 결제 요청

### 베네피아 포인트를 이용하여 결제를 요청합니다.

{% swagger method="post" path="/benepia/payment" baseUrl="https://api.iamport.kr" summary="베네피아 포인트 결제요청" %}
{% swagger-description %}
사용자로부터 전달받은 베네피아 계정 아이디, 비밀번호와 함께 결제정보를 요청하여 베네피아 포인트 사용처리합니다. 

**KCP를 통해서만 진행**

되므로 KCP사이트코드 발급이 필요합니다.
{% endswagger-description %}

{% swagger-parameter in="body" name="benepia_user" type="String" required="true" %}
<mark style="color:red;">

**베네피아 계정 아이디**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="benepia_password" type="String" required="true" %}
<mark style="color:red;">

**베네피아 계정 비밀번호**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="merchant_uid" type="String" required="true" %}
<mark style="color:red;">

**주문번호**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="double" required="true" %}
<mark style="color:red;">

**결제요청금액**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="String(40)" required="true" %}
<mark style="color:red;">

**제품명**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_name" type="String(16)" %}
**구매자명**
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
**PG구분코드**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notice_url" type="String" %}
**Notification URL(Webhook URL)**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_data" type="Array" %}
**에코항목**
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
{% tabs %}
{% tab title="PaymentResponse" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`response`** <mark style="color:red;">**`(PaymentAnnotation, optional)`**</mark>
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="PaymentAnnotation" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**`응답코드`**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`응답메세지`**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`imp_uid`** <mark style="color:red;">\*</mark> <mark style="color:green;">**string**</mark>

**`아임포트 결제 고유 UID`**

&#x20;****&#x20;

**`merchant_uid`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`주문번호`**

****

**`pay_method`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`결제수단 구분코드`**

&#x20;****&#x20;

**`channel`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`결제환경 구분코드`**

* pc **:** (인증방식)PC결제
* mobile:(인증방식)모바일결제
* api:정기결제 또는 비인증 결제



**`pg_provider`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`PG사 구분코드`**

***

**`emb_pg_provider`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`허브형결제 PG사 구분코드`**



**`pg_tid`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**`pg사 거래번호`**

****

**`pg_id`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`PG사 MID`**

****

**`escrow`  ** <mark style="color:orange;">**boolean**</mark>

**`에스크로 결제여부`**

****

**`apply_num`**  ** **<mark style="color:green;">**string**</mark>

**`신용카드 승인번호`**

****

**`bank_code`**  <mark style="color:red;">****</mark>** **<mark style="color:green;">**string**</mark>

**`은행 표준코드`**[**`(링크보기)`**](../../../tip/pg-1.md)**``**

****

**`bank_name`**  <mark style="color:red;">****</mark>** **<mark style="color:green;">**string**</mark>

**`은행 명칭`**

***

**`card_code`**  <mark style="color:red;">****</mark>** **<mark style="color:green;">**string**</mark>

**`카드사 코드번호`(금융결제원 표준코드번호 :** [<mark style="color:red;">**링크**</mark>](https://chaifinance.notion.site/53589280bbc94fab938d93257d452216?v=eb405baf52134b3f90d438e3bf763630) )



**`card_name`**  <mark style="color:green;">**string**</mark>

**`카드사명`**

****

**`card_quota`** ** **<mark style="color:purple;">**integer**</mark>

**`할부개월 수`(0이면 일시불)**

****

**`card_number`** <mark style="color:green;">**string**</mark>

**`마스킹 카드번호`**

***

**`card_type`**  <mark style="color:green;">**string**</mark>

**`카드 구분코드`**

* 0 : 신용카드
* 1 : 체크카드



**`vbank_code`** ** **<mark style="color:green;">**string**</mark>

**`가상계좌 은행 표준코드`(하단이미지 참고)**

***

**`vbank_name`** ** **<mark style="color:green;">**string**</mark>** **&#x20;

**`입금받을 가상계좌 은행명`**

****

**`vbank_holder`**  <mark style="color:green;">**string**</mark>

**`입금받을 가상계좌 예금주`**

****

**`vbank_date`** ** **<mark style="color:green;">**string**</mark>

**`입금받을 가상계좌 마감기한` (UNIX timestamp)**

****

**`vbank_issued_at`** ** **<mark style="color:green;">**string**</mark>

**`가상계좌 생성 시각` (UNIX timestamp)**

****

**`name`    **<mark style="color:green;">**string**</mark>

**`제품명`**

****

**`amount`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:purple;">**integer**</mark>

**`주문(결제)금액`**

&#x20;****&#x20;

**`cancel_amount`** ** **<mark style="color:purple;">**integer**</mark>

**`결제취소금액`**

****

**`currency`    **<mark style="color:green;">**string**</mark>

**`통화구분코드`**

* USD
* KRW
* EUR

***

**`buyer_name`    **<mark style="color:green;">**string**</mark>

**`주문자명`**

****

**`buyer_email`    **<mark style="color:green;">**string**</mark>

**`주문자 Email주소`**\
****

**`buyer_tel`    **<mark style="color:green;">**string**</mark>

**`주문자 전화번호`**

****

**`buyer_addr`    **<mark style="color:green;">**string**</mark>

**`주문자 주소`**

****

**`buyer_postcode`    **<mark style="color:green;">**string**</mark>

**`주문자 우편번호`**

****

**`custom_data`    **<mark style="color:green;">**string**</mark>

**`echo data` **&#x20;

JSON string으로 전달

****

**`user_agent`    **<mark style="color:green;">**string**</mark>

**UserAgent**

결제를 시작한 단말기 **정**



**`status`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`결제상태 구분코드`**

* ready
* paid
* cancelled
* failed



**`started_at`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**`결제시작시점` (UNIX timestamp)**

****

**`paid_at`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`결제완료시점` (UNIX timestamp)**\
****

**`failed_at`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`결제실패시점` (UNIX timestamp)**

****

**`cancelled_at`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`결제취소시점` (UNIX timestamp)**

****

**`fail_reason`** <mark style="color:green;">**string**</mark>

**`결제실패 사유`**

****

**`cancel_reason`**  <mark style="color:green;">**string**</mark>

**`결제취소 사유`**

****

**`receipt_url`**  <mark style="color:green;">**string**</mark>

**`신용카드 매출전표 확인 URL`**

****

**`cash_receipt_issued`  **<mark style="color:orange;">**boolean**</mark>

**`현금영수증 자동발급 여부`**

****

**`customer_uid`    **<mark style="color:green;">**string**</mark>

**해당 결제처리에 사용된 customer\_uid**

****

**`customer_uid_usage`    **<mark style="color:green;">**string**</mark>

**`customer_uid 사용 구분코드`**

* issue **: 빌링키 발급**
* payment : 결제
* payment.scheduled : 예약결제

****

**`cancel_history` ** <mark style="color:red;">**(Array\[PaymentCancelAnnotation], optional):**</mark>

**`취소/부분취소 내역`**
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="PaymentCancelAnnotation" %}
**`pg_tid`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**PG사 승인취소번호**

****

**`amount`  **<mark style="color:red;">**\***</mark> <mark style="color:purple;">**integer**</mark>

**취소 금액**

****

**`cancelled_at`  **<mark style="color:red;">**\***</mark> <mark style="color:green;">**string**</mark>

결제취소된 시각 UNIX timestamp



**`reason`** <mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**결제취소 사유**

****

**`receipt_url`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**취소에 대한 매출전표 확인 URL. PG사에 따라 제공되지 않는 경우도 있음**
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

{% swagger-response status="500: Internal Server Error" description="베네피아 포인트 결제 실패" %}
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
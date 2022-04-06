---
description: 저장된 빌링키(customer_uid)를 이용하여 결제를 요청할 수 있는 API 명세를 기술합니다.
---

# ⌨ 비 인증 결제(빌링키) API

### 저장된 빌링키(customer\_uid)로 결제를 요청 할수 있습니다.

{% swagger method="post" path="/subscribe/payments/again" baseUrl="https://api.iamport.kr" summary="customer_uid 로 결제를 요청합니다." %}
{% swagger-description %}
빌링키 발급 API 또는 PG사 빌링키 발급 결제창에서 설정한

**customer\_uid**

로 비 인증 결제를 요청할 수 있습니다.
{% endswagger-description %}

{% swagger-parameter in="body" name="customer_uid" type="String" required="true" %}
실 빌링키와 1:1로 매칭될 고유번호
{% endswagger-parameter %}

{% swagger-parameter in="body" name="merchant_uid" type="String" required="true" %}
주문번호
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="String" required="false" %}
결제 통화코드
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="integer" required="true" %}
결제금액
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tax_free" type="integer" required="false" %}
면세금액
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="String" required="true" %}
제품명
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_name" type="String" required="false" %}
주문자명
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_email" type="String" required="false" %}
주문자 E-mail주소
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_tel" type="String" required="false" %}
주문자 전화번호
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_addr" type="String" required="false" %}
주문자 주소
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_postcode" type="String" required="false" %}
주문자 우편번호
{% endswagger-parameter %}

{% swagger-parameter in="body" name="card_quota" type="integer" required="false" %}
카드 할부개월수
{% endswagger-parameter %}

{% swagger-parameter in="body" name="interest_free_by_merchant" type="boolean" required="false" %}
가맹점부담 무이자 할부여부
{% endswagger-parameter %}

{% swagger-parameter in="body" name="use_card_point" type="boolean" required="false" %}
카드포인트 사용여부
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_data" type="String" required="false" %}
에코항목
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notice_url" type="String" required="false" %}
결제성공 시 통지될 웹훅 URL
{% endswagger-parameter %}

{% swagger-parameter in="body" name="browser_ip" type="String" required="false" %}
구매자 브라우져(PC)의 IP
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="결제성공" %}
{% tabs %}
{% tab title="Model" %}
**code **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**message **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**imp\_uid** <mark style="color:red;">\*</mark> <mark style="color:green;">**string**</mark>

**아임포트 결제 고유 UID**

****

**merchant\_uid **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**주문번호**

****

**pay\_method **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**결제수단 구분코드**

****

**channel **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**결제환경 구분코드**

* pc **:** (인증방식)PC결제
* mobile:(인증방식)모바일결제
* api:정기결제 또는 비인증 결제



**pg\_provider **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**PG사 구분코드**

***

**emb\_pg\_provider **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**허브형결제 PG사 구분코드**



**pg\_tid **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**pg사 거래번호**

****

**pg\_id **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**PG사 MID**

****

**escrow** boolean

**에스크로 결제여부**

****

**apply\_num**  ** **<mark style="color:green;">**string**</mark>

**신용카드 승인번호**

****

**bank\_code**  <mark style="color:red;">****</mark>** **<mark style="color:green;">**string**</mark>

**은행 표준코드(링크보기)**

****

**bank\_name**  <mark style="color:red;">****</mark>** **<mark style="color:green;">**string**</mark>

**은행 명칭**

***

**card\_code**  <mark style="color:red;">****</mark>** **<mark style="color:green;">**string**</mark>

**카드사 코드번호(금융결제원 표준코드번호 :** [<mark style="color:red;">**링크**</mark>](https://chaifinance.notion.site/53589280bbc94fab938d93257d452216?v=eb405baf52134b3f90d438e3bf763630) )



**card\_name**  <mark style="color:green;">**string**</mark>

**카드사명**

****

**card\_quota** ** **<mark style="color:purple;">**integer**</mark>

**할부개월 수(0이면 일시불)**

****

**card\_number** <mark style="color:green;">**string**</mark>

**마스킹 카드번호**

***

**card\_type** \*<mark style="color:green;">**string**</mark>

**카드 구분코드**

* 0 : 신용카드
* 1 : 체크카드



**vbank\_code** ** **<mark style="color:green;">**string**</mark>

**가상계좌 은행 표준코드(하단이미지 참고)**

***

**vbank\_name** ** **<mark style="color:green;">**string**</mark>** **&#x20;

**입금받을 가상계좌 은행명**

****

**vbank\_holder**  <mark style="color:green;">**string**</mark>

**입금받을 가상계좌 예금주**

****

vbank\_date ** **<mark style="color:green;">**string**</mark>

**입금받을 가상계좌 마감기한 (UNIX timestamp)**

****

**vbank\_issued\_at** ** **<mark style="color:green;">**string**</mark>

**가상계좌 생성 시각 (UNIX timestamp)**

****

**name  **<mark style="color:green;">**string**</mark>

**제품명**

****

**amount **<mark style="color:red;">**\***</mark>**  **<mark style="color:purple;">**integer**</mark>

**주문(결제)금액**

****

**cancel\_amount** ** **<mark style="color:purple;">**integer**</mark>

**결제취소금액**

****

**currency  **<mark style="color:green;">**string**</mark>

**통화구분코드**

* USD
* KRW
* EUR

***

**buyer\_name  **<mark style="color:green;">**string**</mark>

**주문자명**

****

**buyer\_email  **<mark style="color:green;">**string**</mark>

**주문자 Email주소**\
****

**buyer\_tel  **<mark style="color:green;">**string**</mark>

**주문자 전화번호**

****

**buyer\_addr  **<mark style="color:green;">**string**</mark>

**주문자 주소**

****

**buyer\_postcode  **<mark style="color:green;">**string**</mark>

**주문자 우편번호**

****

**custom\_data  **<mark style="color:green;">**string**</mark>

**echo data JSON string으로 전달**

****

**user\_agent  **<mark style="color:green;">**string**</mark>

**결제를 시작한 단말기의 UserAgent**

****

**status **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**결제상태 구분코드**

* ready
* paid
* cancelled
* failed



**started\_at **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**결제시작시점 (UNIX timestamp)**

****

**paid\_at **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**결제완료시점 (UNIX timestamp)**\
****

**failed\_at **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**결제실패시점 (UNIX timestamp)**

****

**cancelled\_at **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**결제취소시점 (UNIX timestamp)**

****

**fail\_reason** <mark style="color:green;">**string**</mark>

**결제실패 사유**

****

**cancel\_reason**  <mark style="color:green;">**string**</mark>

**결제취소 사유**

****

**receipt\_url**  <mark style="color:green;">**string**</mark>

**신용카드 매출전표 확인 URL**

****

**cash\_receipt\_issued **<mark style="color:orange;">**boolean**</mark>

**현금영수증 자동발급 여부**

****

**customer\_uid  **<mark style="color:green;">**string**</mark>

**해당 결제처리에 사용된 customer\_uid**

****

**customer\_uid\_usage  **<mark style="color:green;">**string**</mark>

**customer\_uid 사용 구분코드**

* issue **: 빌링키 발급**
* payment : 결제
* payment.scheduled : 예약결제



**cancel\_history array \[]**

> **pg\_tid **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>
>
> **PG사 승인취소번호**
>
> ****
>
> **amount **<mark style="color:red;">**\***</mark> <mark style="color:purple;">**integer**</mark>
>
> **취소 금액**
>
> ****
>
> **cancelled\_at **<mark style="color:red;">**\***</mark> <mark style="color:green;">**string**</mark>
>
> 결제취소된 시각 UNIX timestamp
>
>
>
> **reason** <mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>
>
> **결제취소 사유**
>
> ****
>
> **receipt\_url** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>
>
> **취소에 대한 매출전표 확인 URL. PG사에 따라 제공되지 않는 경우도 있음**
{% endtab %}

{% tab title="Model Schema" %}
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

![은행코드표](<../../../.gitbook/assets/image (23).png>)

---
description: 빌링키로 등록된 결졔예약내역을 조회할 수 있습니다.
---

# ⌨ 빌링키 결제예약 조회 API

### 빌링키별 결제예약목록을 조회할 수 있습니다.

{% swagger method="get" path="/subscribe/customers/{customer_uid}/schedules" baseUrl="https://api.iamport.kr" summary="빌링키 결제예약 조회" %}
{% swagger-description %}
결제예약정보가 (페이징된)목록으로 전달되며 최대 3개월 단위로 조회가 가능합니다.
{% endswagger-description %}

{% swagger-parameter in="path" name="customer_uid" type="String" required="true" %}
<mark style="color:red;">

**빌링키**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="integer" %}
**조회목록 페이징**

1부터 시작하며 기본값은 1입니다.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="from" type="integer" required="true" %}
<mark style="color:red;">**조회 시작시각**</mark>** **&#x20;

unix timestamp
{% endswagger-parameter %}

{% swagger-parameter in="query" name="to" type="integer" required="true" %}
<mark style="color:red;">**조회 종료시각**</mark>** **&#x20;

unix timestamp
{% endswagger-parameter %}

{% swagger-parameter in="query" name="schedule-status	" type="String" %}
**예약상태**&#x20;

누락되면 모든 상태의 예약내역 조회

`scheduled`: 예약됨(실행되기 전)

`executed`: 예약된 결제실행완료

`revoked`: 예약철회
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
{% tabs %}
{% tab title="Model" %}
**`code`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:purple;">**integer**</mark>

**`응답코드`**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**`응답메세지`**

code값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`customer_uid`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**`빌링키`**

****

**`merchant_uid`  \*  **<mark style="color:green;">**string**</mark>

**`주문번호`**



**`imp_uid`** <mark style="color:red;">\*</mark> <mark style="color:green;">**string**</mark>

**`아임포트 결제 고유 UID`**

&#x20;****&#x20;

**`schedule_at`    **<mark style="color:red;">**\***</mark>**    **<mark style="color:blue;">**UNIX timestamp**</mark>** **&#x20;

**`예약결제 실행 예정 시각`**&#x20;

&#x20;****&#x20;

**`executed_at`  **<mark style="color:red;">**\***</mark>**    **<mark style="color:blue;">**UNIX timestamp**</mark>

**`예약결제가 실행된 시각`` `**<mark style="color:blue;">**``**</mark>&#x20;

&#x20;<mark style="color:blue;">****</mark>&#x20;

**`revoked_at`  **<mark style="color:red;">**\***</mark>**    **<mark style="color:blue;">**UNIX timestamp**</mark>

**`예약결제 실행을 철회한 시각`` `**<mark style="color:blue;">**``**</mark>&#x20;

&#x20;<mark style="color:blue;">****</mark>&#x20;

**`amount`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:purple;">**integer**</mark>

**`주문(결제)금액`**

&#x20; **** &#x20;

**`name`    **<mark style="color:green;">**string**</mark>

**`제품명`**

****

**`buyer_name`    **<mark style="color:green;">**string**</mark>

**`주문자명`**

****

**`buyer_email`    **<mark style="color:green;">**string**</mark>

**`주문자 Email주소`**\
**`` **&#x20;

**`buyer_tel`    **<mark style="color:green;">**string**</mark>

**`주문자`  `전화번호`**

****

**`buyer_addr`    **<mark style="color:green;">**string**</mark>

**`주문자 주소`**

&#x20;****&#x20;

**`buyer_postcode`    **<mark style="color:green;">**string**</mark>

**`주문자 우편번호`**

&#x20;****&#x20;

**`custom_data`    **<mark style="color:green;">**string**</mark>

**`echo data` **&#x20;

JSON string으로 전달

****

**`schedule_status`  **<mark style="color:blue;">****</mark>**  **<mark style="color:red;">**\***</mark>**  **<mark style="color:blue;">****</mark>** **<mark style="color:green;">**string**</mark>

**`예약상태` **<mark style="color:green;">****</mark>&#x20;

* `scheduled`: 예약됨(실행되기 전)
* `executed`: 예약된 결제실행완료
* `revoked`: 예약철회



**`payment_status` **<mark style="color:green;">****</mark>** **<mark style="color:red;">**\***</mark>**  **<mark style="color:blue;">****</mark>** **<mark style="color:green;">**string**</mark>

**`실행된 결제의 승인 상태`` `**<mark style="color:green;">**``**</mark>&#x20;

* `null`: 아직 예약결제가 실행되지 않음(null 이라는 값의 문자열이 아닌 실제 null 입니다)
* `paid`: 예약결제가 결제승인됨
* `failed`: 예약결제가 승인실패됨
* `cancelled`: 예약결제가 결제승인 후 환불됨



**`fail_reason`    **<mark style="color:green;">**string**</mark>

**`실패사유` **<mark style="color:green;">****</mark>&#x20;
{% endtab %}

{% tab title="Model Schema" %}
```json
{
  "code": 0,
  "message": "string",
  "response": [
    {
      "customer_uid": "string",
      "merchant_uid": "string",
      "imp_uid": "string",
      "schedule_at": "0",
      "executed_at": "0",
      "revoked_at": "0",
      "amount": 0,
      "name": "string",
      "buyer_name": "string",
      "buyer_email": "string",
      "buyer_tel": "string",
      "buyer_addr": "string",
      "buyer_postcode": "string",
      "custom_data": "string",
      "schedule_status": "scheduled",
      "payment_status": "paid",
      "fail_reason": "string"
    }
  ]
}
```
{% endtab %}
{% endtabs %}
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="검색 파라메터가 유효하지 않은 경우" %}
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

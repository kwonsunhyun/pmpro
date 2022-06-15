---
description: 페이먼트월 PG 사 이용시 실물상품 배송등록을 수행합니다.
---

# ⌨ 페이먼트월 배송등록 API

### 배송정보를 등록합니다.

이커머스(실물 상품) 비즈니스의 경우 페이먼트월에서 필수적으로 요구되는 배송정보 등록 API

{% swagger method="post" path="/paymentwall/delivery" baseUrl="https://api.iamport.kr" summary="실물상품 배송정보를 등록합니다." %}
{% swagger-description %}
해당 배송등록을 누락한 경우 페이먼트월 PG사로부터 정산대금을 받지 못합니다.
{% endswagger-description %}

{% swagger-parameter in="body" name="imp_uid" type="String" required="true" %}
<mark style="color:red;">

**아임포트 거래번호**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="merchant_uid" type="String(40)" required="true" %}
<mark style="color:red;">

**주문번호**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="String(10)" required="true" %}
<mark style="color:red;">**상품구분코드**</mark>

**`physical:실물`**

**`digital:디지털` **<mark style="color:red;">****</mark>&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="status" type="String(10)" required="true" %}
<mark style="color:red;">**배송상태 구분코드**</mark>

**`order_placed`**

**`order_shipped`**

**`delivering`**

**`delivered` **<mark style="color:red;">****</mark>&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="carrier_tracking_id" type="String(64)" %}
**운송장 번호**&#x20;

physical 주문인 경우 필수 파라미터
{% endswagger-parameter %}

{% swagger-parameter in="body" name="carrier_type" type="String(64)" %}
**운송사 이름**&#x20;

physical 주문인 경우 필수 파라미터
{% endswagger-parameter %}

{% swagger-parameter in="body" name="estimated_delivery_datetime" type="integer" %}
**도착예상시간**&#x20;

Unix timestamp&#x20;

(digital 인 경우 현 시간을 기록해도 무방)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="estimated_update_datetime" type="integer" %}
**배송상태 업데이트 예정시간**

Unix timestamp sec&#x20;

(digital 인 경우 지금 시간을 기록해도 무방)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="reason" type="String(64)" %}
**사유**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="refundable" type="String" required="true" %}
<mark style="color:red;">**환불가능여부**</mark>

`yes`

`no`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="details" type="String(400)" %}
**상세 사항**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="shipping_address_email" type="String(50)" required="true" %}
<mark style="color:red;">

**수신자 email**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="shipping_address_country" type="String(40)" %}
**수신자 국가**&#x20;

(physical 주문인 경우 필수 파라미터)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="shipping_address_city" type="String(40)" %}
**수신자 시**&#x20;

(physical 주문인 경우 필수 파라미터)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="shipping_address_zip" type="String(40)" %}
**수신자 우편번호**&#x20;

(physical 주문인 경우 필수 파라미터)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="shipping_address_state" type="String(40)" %}
**수신자 주**

미국이 아닌 경우 'N/A'로 표기&#x20;

(physical 주문인 경우 필수 파라미터)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="shipping_address_street" type="String(40)" %}
**수신자 거리명**&#x20;

(physical 주문인 경우 필수 파라미터)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="shipping_address_phone" type="String(40)" %}
**수신자 전화번호**&#x20;

(physical 주문인 경우 필수 파라미터)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="shipping_address_firstname" type="String(40)" %}
**수신자 이름**&#x20;

(physical 주문인 경우 필수 파라미터)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="shipping_address_lastname" type="String(40)" %}
**수신자 성**&#x20;

(physical 주문인 경우 필수 파라미터)
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
{% tabs %}
{% tab title="PaymentwallDeliveryAnnotation" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**response** <mark style="color:red;">**(PaymentwallDeliveryDetailAnnotation, optional):**</mark>&#x20;

에러 메시지를 포함하거나, 성공시 success: 1 메시지를 포함합니다.
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="PaymentwallDeliveryDetailAnnotation" %}
**`error_code`**<mark style="color:orange;">**`integer`**</mark>

이 값이 없으면 정상적인 경우, 없으면 notices를 확인해봐야 합니다



**`error`` `**<mark style="color:green;">**`string`**</mark>

**`에러 메시지`**

&#x20;****&#x20;

**`notices`` `**<mark style="color:yellow;background-color:yellow;">**`Array[string]`**</mark>

**`자세한 에러 메시지`**
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

<details>

<summary>Response Model Schema</summary>

```json
{
  "code": 0,
  "message": "string",
  "response": {
    "error_code": 0,
    "error": "string",
    "notices": [
      "string"
    ]
  }
}
```

</details>

{% hint style="success" %}
**Swagger Test Link**

****[**https://api.iamport.kr/#!/paymentwall/paymentwall\_delivery**](https://api.iamport.kr/#!/paymentwall/paymentwall\_delivery)****
{% endhint %}

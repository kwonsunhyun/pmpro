---
description: 예약된 결제내역을 취소할 수 있는 API 입니다.
---

# ⌨ 결제 예약취소 API

### 예약된 결제가 실행되기전에 해당 예약을 취소할 수 있는 API 입니다.

{% swagger method="post" path="/subscribe/payments/unschedule" baseUrl="https://api.iamport.kr" summary="예약된 결제를 취소합니다." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" required="true" name="customer_uid" type="String" %}
<mark style="color:red;">

**빌링키**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="merchant_uid" type="Array" %}
**주문번호**

누락되면 customer\_uid에 대한 결제 예약정보 일괄취소
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

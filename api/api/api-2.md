---
description: 예약된 결제내역을 조회할 수 있는 API 입니다.
---

# ⌨ 결제예약 복수조회 API

### 기간범위를 지정하여 결제예약목록을 조회할 수 있습니다.

{% swagger method="get" path="/subscribe/payments/schedule" baseUrl="https://api.iamport.kr" summary="예약된 결재내역 조회 API" %}
{% swagger-description %}
결제예약정보가 예약된 시각 기준으로 최신순으로 정렬되어 전달됩니다. 과거순으로 정렬하기 위해서는 

**sorting=scheduled**

 파라메터를 지정하시면 됩니다.
{% endswagger-description %}

{% swagger-parameter in="body" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
```javascript
{
    // Response
}
```
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

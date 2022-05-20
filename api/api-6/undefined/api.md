---
description: 주문내역을 조회 합니다.
---

# ⌨ 주문내역 조회 API

### &#x20;[카카오페이 주문내조회 API](https://developers.kakao.com/docs/restapi/kakaopay-api#%EC%A3%BC%EB%AC%B8%EB%82%B4%EC%97%AD%EC%A1%B0%ED%9A%8C)를 래핑한 API 입니다.

{% swagger method="get" path="/kakao/payment/orders" baseUrl="https://api.iamport.kr" summary="주문내역 조회 API" %}
{% swagger-description %}
지원되는 request가 유사하며 응답되는 response는 카카오페이 API 와 동일합니다.
{% endswagger-description %}

{% swagger-parameter in="query" name="payment_request_date" type="String" required="true" %}
&#x20;<mark style="color:red;">**요청일자**</mark>&#x20;

YYYYMMDD 형식의 조회 날짜를 지정하시면 됩니다.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="cid" type="String" %}
**카카오페이 MID**

아임포트 내 설정된 카카오페이 CID를 기본값으로 합니다.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="integer" %}
**페이지 번호**

 
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

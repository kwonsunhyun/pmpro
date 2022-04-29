---
description: customer_uid 기준으로 예약된 내역을 조회할 수 있는 API 입니다.
---

# ⌨ 결제예약 복수조회(빌키) API

### customer\_uid 별 결제예약목록을 조회할 수 있습니다

{% swagger method="get" path="/subscribe/payments/schedule/customers/{customer_uid}" baseUrl="https://api.iamport.kr" summary="빌키(customer_uid) 기준 결제내역 복수조회 API" %}
{% swagger-description %}
결제예약정보가 목록으로 전달되며 최대 3개월 단위로 조회가 가능합니다.
{% endswagger-description %}

{% swagger-parameter in="path" name="customer_uid" type="String" required="true" %}
<mark style="color:red;">

**빌키**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="integer" %}
**조회목록 페이징**

1부터 시작하며, 기본값은 1입니다.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="from" type="integer" required="true" %}
<mark style="color:red;">**조회 시작시각**</mark>&#x20;

unix timestamp
{% endswagger-parameter %}

{% swagger-parameter in="query" name="to" type="integer" required="true" %}
<mark style="color:red;">**조회 종료시각**</mark>&#x20;

unix timestamp
{% endswagger-parameter %}

{% swagger-parameter in="query" name="schedule-status" type="String" %}
**예약상태**

누락되면 모든 상태의 예약내역 조회

`scheduled`: 예약됨(실행되기 전)

`executed`: 예약된 결제실행완료

`revoked`: 예약철회
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

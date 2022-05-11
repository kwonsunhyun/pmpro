---
description: 가상계좌번호를 발급하여 고객이 입금할수 있도록 합니다.
---

# ⌨ 가상계좌 발급 API

### 가상계좌번호를 발급할수 있습니다.

해당 API 는 아래 PG사를 이용하는 경우에만 사용 가능합니다.

* 세틀뱅크
* 나이스페이먼츠
* KG이니시스

{% swagger method="post" path="/vbanks" baseUrl="https://api.iamport.kr" summary="가상계좌 번호를 발급합니다." %}
{% swagger-description %}
희망하시는 은행, 예금주명으로 입금이 가능한 가상계좌를 생성할 수 있습니다.(별도로 PG계약 필요)


{% endswagger-description %}

{% swagger-parameter in="body" name="merchant_uid" type="String" required="true" %}
<mark style="color:red;">

**주문번호**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="Double" required="true" %}
<mark style="color:red;">

**발급금액**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="vbank_code" type="String" required="true" %}
<mark style="color:red;">

**은행구분코드**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="vbank_due" %}

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

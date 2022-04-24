---
description: 본인인증 결과를 조회합니다.
---

# ⌨ 본인인증 결과조회 API

### 본인인증된 결과를 조회할 때 사용합니다.

{% swagger method="get" path="/certifications/{imp_uid}" baseUrl="https://api.iamport.kr" summary="본인인증 결과를 imp_uid를 이용하여 조회합니다." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" required="true" name="imp_uid" type="String" %}
<mark style="color:red;">

**차이포트 인증고유번호**

</mark>
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="조회성공" %}
{% tabs %}
{% tab title="Model" %}
**`imp_uid`**  <mark style="color:red;">\*</mark> <mark style="color:green;">**string**</mark>&#x20;

**`인증고유번호`**

****

**`merchant_uid`    **<mark style="color:green;">**string**</mark>

**`주문번호`**

****

**`pg_tid`  **<mark style="color:blue;">****</mark>**  **<mark style="color:green;">**string**</mark>

**`PG사 인증결과 고유번호` **&#x20;

****

**`pg_provider`** <mark style="color:red;">**\***</mark>**  **<mark style="color:green;">****</mark>  <mark style="color:green;"></mark><mark style="color:green;">string</mark>&#x20;

**`본인인증 제공 PG사 명칭`**

&#x20;
{% endtab %}

{% tab title="Model Schema" %}
```
{
  "code": 0,
  "message": "string",
  "response": {
    "imp_uid": "string",
    "merchant_uid": "string",
    "pg_tid": "string",
    "pg_provider": "string",
    "name": "string",
    "gender": "string",
    "birth": 0,
    "birthday": "string",
    "foreigner": true,
    "phone": "string",
    "carrier": "SKT",
    "certified": true,
    "certified_at": 0,
    "unique_key": "string",
    "unique_in_site": "string",
    "origin": "string",
    "foreigner_v2": true
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

{% swagger-response status="404: Not Found" description="휴대폰 본인인증결과를 찾을 수 없음" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

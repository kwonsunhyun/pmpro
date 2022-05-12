---
description: 발급된 빌링키 정보를 확인할 수 있습니다.
---

# ⌨ 빌링키 정보 단건조회 API

### 구매자의 빌링키 단건 정보를 조회 합니다.

{% swagger method="get" path="/subscribe/customers/{customer_uid}" baseUrl="https://api.iamport.kr" summary="구매자의 빌링키 정보 조회" %}
{% swagger-description %}
빌링키 정보를 확인할 수 있습니다.
{% endswagger-description %}

{% swagger-parameter in="path" name="customer_uid" type="String" required="true" %}
<mark style="color:red;">

**빌링키**

</mark>
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
{% tabs %}
{% tab title="CustomerResponse" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`response`** <mark style="color:red;">**(CustomerAnnotation, optional)**</mark>
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="CustomerAnnotation" %}
**`code`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:purple;">**integer**</mark>

**`응답코드`**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**`응답메세지`**

code값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`customer_uid`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**`고객 고유번호`**\
****

**`pg_provider`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**빌링키가 등록된 PG사 코드**

****

**`pg_id`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**빌링키가 등록된 PG사 상점아이디(MID)**

****

**`card_name`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**`카드사명`**

****

**`card_code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`카드사 코드`**

&#x20;****&#x20;

**`card_number`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`마스킹 카드번호`**

****

**`card_type`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`카드유형`**

**(주의)해당 정보를 제공하지 않는 일부 PG사의 경우 null 로 응답됨**

****

**`customer_name`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`고객성함`**

****

**`customer_tel`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**`고객 전화번호`**

****

**`customer_email`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`고객 Email`**

****

**`customer_addr`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`고객 주소` **&#x20;

&#x20;

**`customer_postcode`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`고객 우편번호`**



**`inserted`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**`빌키가 등록된 시각`** UNIX timestamp



**`updated`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**`빌키가 업데이트된 시각`** UNIX timestamp
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

{% swagger-response status="404: Not Found" description="유효하지 않은 customer_uid" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

### Response Model Schema

<details>

<summary>HTTP status 200</summary>

```json
{
  "code": 0,
  "message": "string",
  "response": {
    "customer_uid": "string",
    "pg_provider": "string",
    "pg_id": "string",
    "card_name": "string",
    "card_code": "string",
    "card_number": "string",
    "card_type": "null",
    "customer_name": "string",
    "customer_tel": "string",
    "customer_email": "string",
    "customer_addr": "string",
    "customer_postcode": "string",
    "inserted": 0,
    "updated": 0
  }
}
```

</details>

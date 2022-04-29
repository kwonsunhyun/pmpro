---
description: 복수개의 빌링키를 이용하여 빌링키 정보를 조회할수 있습니다.
---

# ⌨ 빌링정보 복수조회 API

### 복수개의 빌링키 정보를 입력하여 각각의 빌링키 정보를 조회할 수 있습니다.

{% swagger method="get" path="/subscribe/customers" baseUrl="https://api.iamport.kr" summary="빌링정보 복수조회 API" %}
{% swagger-description %}
등록된 카드마다 1개의 customer_uid가 매핑되므로 가맹점 시스템 내에 1명의 고객이 여러 장의 카드를 등록할 수 있는 경우 여러 개의 customer_uid를 가지게 됩니다. 해당 고객이 등록한 카드정보 목록을 한 번에 조회하는데 사용하면 편리합니다.
{% endswagger-description %}

{% swagger-parameter in="query" name="customer_uid[]" type="Array" required="true" %}
<mark style="color:red;">

**빌키**

</mark>
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
{% tabs %}
{% tab title="Model" %}
**`code`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:purple;">**`integer`**</mark><mark style="color:purple;">** **</mark><mark style="color:purple;">****</mark>&#x20;

**`응답코드`**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>** **&#x20;

**`응답메세지`**

code값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`customer_uid`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**`string`**</mark>

**`빌링키`**

****

**`pg_provider`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**`string`**</mark>

**`PG사 구분코드` **<mark style="color:purple;">****</mark>&#x20;

<mark style="color:purple;">****</mark>

**`pg_id`` `**<mark style="color:red;">**`*`**</mark>**` `**<mark style="color:green;">**`string`**</mark><mark style="color:green;">** **</mark><mark style="color:green;">****</mark>&#x20;

**`PG사 MID`**

**``**

**`card_name`**<mark style="color:green;">**`string`**</mark>** **&#x20;

**`카드사명`**&#x20;

****

**`card_code`**<mark style="color:green;">**`string`**</mark>

**`카드사 코드번호`**

(금융결제원 표준코드번호 **:** [<mark style="color:red;">**링크**</mark>](https://chaifinance.notion.site/53589280bbc94fab938d93257d452216?v=eb405baf52134b3f90d438e3bf763630) )



**`card_number`**<mark style="color:green;">**`string`**</mark>

**`마스킹 카드번호`**

****

**`card_type`**  <mark style="color:green;">**`string`**</mark>** **&#x20;

**`카드 구분코드`**

* 0 : 신용카드
* 1 : 체크카드



**`customer_name`    **<mark style="color:green;">**`string`**</mark><mark style="color:green;">**  **</mark><mark style="color:green;">****</mark> &#x20;

**`고객(카드소지자) 관리용 성함`**

****

**`customer_tel`    **<mark style="color:green;">**`string`**</mark><mark style="color:green;">**  **</mark><mark style="color:green;">****</mark> &#x20;

**`고객(카드소지자) 전화번호`**

**``**

**`customer_email`  **<mark style="color:purple;">****</mark>**  **<mark style="color:green;">**`string`**</mark>

**`고객(카드소지자) Email`**

**``**

**`customer_addr`    **<mark style="color:green;">**`string`**</mark>

**`고객(카드소지자) 주소` **<mark style="color:green;">****</mark>&#x20;

<mark style="color:green;">****</mark>

**customer\_postcode  **<mark style="color:green;">****</mark><mark style="color:green;">**  **</mark><mark style="color:green;">**`string`**</mark>

**`고객(카드소지자) 우편번호` **<mark style="color:green;">****</mark>&#x20;

<mark style="color:green;">****</mark>

**`inserted`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**`integer`**</mark>

빌키가 등록된 시각 UNIX timestamp

<mark style="color:green;">****</mark>

**`updated`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**`integer`**</mark>

빌키가 업데이트된 시각 UNIX timestamp
{% endtab %}

{% tab title="Model Schema" %}
```
{
  "code": 0,
  "message": "string",
  "response": [
    {
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
  ]
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

{% swagger-response status="404: Not Found" description="유효하지 않은 customer_uid" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

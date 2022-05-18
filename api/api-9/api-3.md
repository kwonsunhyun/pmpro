---
description: 은행코드 및 계좌번호를 이용하여 예금주 성명을 조회합니다.
---

# ⌨ 예금주 조회 API

### &#x20;예금주 성명을 은행계좌번호를 이용하여 획득합니다.

{% swagger method="get" path="/vbanks/holder" baseUrl="https://api.iamport.kr" summary="은행코드, 계좌번호를 이용해 해당 계좌의 예금주 명을 조회합니다." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="bank_code" type="String" required="true" %}
<mark style="color:red;">

**은행코드**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="query" name="bank_num" type="String" required="true" %}
<mark style="color:red;">**계좌번호**</mark>

`숫자외 기호 포함 가능`
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
{% tabs %}
{% tab title="VbankHolderResponse" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**response **<mark style="color:red;">**(VbankHolderAnnotation, optional)**</mark>
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="VbankHolderAnnotation" %}
**`bank_holder`` `**<mark style="color:red;">**`*`**</mark>**` `**<mark style="color:green;">**`string`**</mark>

**`예금주명`**
{% endtab %}
{% endtabs %}
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="bank_code가 누락된 경우" %}
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

{% swagger-response status="404: Not Found" description="계좌정보 조회 실패" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

### Respose Model Schema

<details>

<summary>HTTP status 200</summary>

```json
{
  "code": 0,
  "message": "string",
  "response": {
    "bank_holder": "string"
  }
}
```

</details>

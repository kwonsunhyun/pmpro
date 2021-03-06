---
description: 은행표준코드, 은행명을 조회할 수 있습니다
---

# ⌨ 은행명 단건조회 API

### 은행코드로 은행명을 획득합니다.

{% swagger method="get" path="/banks/{bank_standard_code}" baseUrl="https://api.iamport.kr" summary="은행코드로 은행명을 획득합니다." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="bank_standard_code	" type="String" required="true" %}
<mark style="color:red;">

**은행코드**

</mark>
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
{% tabs %}
{% tab title="StandardCodeListResponse" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`response`**<mark style="color:red;">**`(Array[StandardCodeAnnotation], optional)`**</mark><mark style="color:red;">** **</mark><mark style="color:red;">****</mark>&#x20;
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="StandardCodeAnnotation" %}
**`code`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**`기관코드(금융결제원표준코드)`**

&#x20;****&#x20;

**`name`` `**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**`기관명(금융결제원기재명)`**
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

{% swagger-response status="404: Not Found" description="코드에 해당되는 은행정보를 찾을 수 없음" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

<details>

<summary>Response Model Schema</summary>

```
{
  "code": 0,
  "message": "string",
  "response": {
    "code": "string",
    "name": "string"
  }
}
```

</details>

{% hint style="success" %}
**Swagger Test Link**

****[**https://api.iamport.kr/#!/codes/bankCodes**](https://api.iamport.kr/#!/codes/bankCodes)****
{% endhint %}

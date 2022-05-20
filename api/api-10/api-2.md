---
description: 은행정보 리스트를 조회합니다.
---

# ⌨ 은행코드 전체조회 API

### 은행표준코드, 은행명을 모두 조회할 수 있습니다(금융결제원표준코드 기준)

{% swagger method="get" path="/banks" baseUrl="https://api.iamport.kr" summary="은행표준코드, 은행명을 모두 조회할 수 있습니다" %}
{% swagger-description %}

{% endswagger-description %}

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
  "response": [
    {
      "code": "string",
      "name": "string"
    }
  ]
}
```

</details>

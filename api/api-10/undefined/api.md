---
description: 베네피아 포인트를 단건 조회 합니다.
---

# ⌨ 포인트 단건조회 API

### API를 통해 베네피아 포인트(복지포인트)단건 조회

{% swagger method="post" path="/benepia/point" baseUrl="https://api.iamport.kr" summary="베네피아 포인트(복지포인트)단건 조회" %}
{% swagger-description %}
사용자로부터 베네피아 계정 아이디, 비밀번호를 전달받아 보유중인 베네피아 포인트를 조회할 수 있습니다. KCP를 통해서만 진행되므로 KCP사이트코드 발급이 필요합니다.
{% endswagger-description %}

{% swagger-parameter in="body" name="benepia_user" type="String" required="true" %}
<mark style="color:red;">

**베네피아 계정 아이디**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="benepia_password" type="String" required="true" %}
<mark style="color:red;">

**베네피아 계정 비밀번호**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pg" type="String" %}
**PG구분코드**

KCP PG설정이 2개 이상인 경우 **** 조회가 진행되길 원하는 KCP사이트코드를 지정하실 수 있습니다. pg 파라메터는 **kcp.{KCP사이트코드}** 형식의 문자열입니다. pg 파라메터가 누락되는 경우 PG설정 내 KCP설정을 자동 탐색하여 처리하게 됩니다.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
{% tabs %}
{% tab title="BenepiaPointResponse" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`response`` `**<mark style="color:red;">**`(BenepiaPointAnnotation, optional)`**</mark>
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="BenepiaPointAnnotation" %}
**`point`**<mark style="color:red;">**`*`**</mark><mark style="color:orange;">**`integer`**</mark>

**`베네피아 보유 포인트`**
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

{% swagger-response status="500: Internal Server Error" description="베네피아 포인트 조회 실패" %}
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
    "point": 0
  }
}
```

</details>

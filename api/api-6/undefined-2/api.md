---
description: 네이버페이 결제형 에스크로 거래 상태코드를 확정으로 변경합니다.
---

# ⌨ 에스크로 주문확정 API

### 네이버페이 결제형 에스크로 주문 상태 확정 변경 API

{% swagger method="post" path="/payments/{imp_uid}/naver/confirm" baseUrl="https://api.iamport.kr" summary="네이버페이 에스크로 주문 확정" %}
{% swagger-description %}
결제형-네이버페이
{% endswagger-description %}

{% swagger-parameter in="path" name="imp_uid	" type="String" required="true" %}
<mark style="color:red;">

**아임포트 거래번호**

</mark>
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
{% tabs %}
{% tab title="ResponseAnnotation" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다
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

{% swagger-response status="404: Not Found" description="imp_uid에 해당되는 거래건을 찾을 수 없거나 접근 권한이 없는 계정인 경우" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="네이버페이 구매확정 실패. 응답 BODY의 message 확인 필요" %}
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
  "message": "string"
}
```

</details>

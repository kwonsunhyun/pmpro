---
description: 베네피아 포인트를 단건 조회 합니다.
---

# ⌨ 포인트 단건조회 API

### API를 통해 베네피아 포인트(복지포인트)단건 조회

{% swagger method="post" path="/benepia/point" baseUrl="https://api.iamport.kr" summary="베네피아 포인트(복지포인트)단건 조회" %}
{% swagger-description %}
사용자로부터 베네피아 계정 아이디, 비밀번호를 전달받아 보유중인 베네피아 포인트를 조회할 수 있습니다. KCP를 통해서만 진행되므로 KCP사이트코드 발급이 필요합니다.
{% endswagger-description %}

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

{% swagger-response status="500: Internal Server Error" description="베네피아 포인트 조회 실패" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

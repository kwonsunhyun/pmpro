---
description: 관리자 콘솔에 등록한 PG MID 정보를 복수조회 합니다.
---

# ⌨ PG MID 복수조회 API

### PG설정정보 조회 API

{% swagger method="get" path="/users/pg" baseUrl="https://api.iamport.kr" summary="등록된 PG MID 정보를 복수조회 할수 있습니다." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="성공" %}
{% tabs %}
{% tab title="MultiplePgSettingResponse" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`response`**<mark style="color:red;">**`(Array[PgSettingAnnotation], optional)`**</mark>
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="PgSettingAnnotation" %}
**`pg_provider`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**`PG사 구분코드`**

[**코드표 확인**](../../../tip/pg-2.md)****



**`pg_id`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**`PG MID`**



**`sandbox`` `**<mark style="color:red;">**`*`**</mark><mark style="color:orange;">**`boolean`**</mark>

**`테스트모드 여부`**



**`type`` `**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**`PG설정 타입 구분코드`**

* `payment` : 인증방식 결제.(관리자 콘솔에서 PG설정(일반결제 및 정기결제) 탭에 해당) &#x20;
* `api_payment` : API 방식의 결제. (관리자 콘솔에서 PG설정(일반결제 및 키인결제) 탭에 해당)&#x20;
* `certification` : 본인 인증. (관리자 콘솔에서 본인 인증 서비스 탭에 해당)
{% endtab %}
{% endtabs %}
{% endswagger-response %}
{% endswagger %}

<details>

<summary>Response Model Schema</summary>

```json
{
  "code": 0,
  "message": "string",
  "response": [
    {
      "pg_provider": "string",
      "pg_id": "string",
      "sandbox": true,
      "type": "payment"
    }
  ]
}
```

</details>
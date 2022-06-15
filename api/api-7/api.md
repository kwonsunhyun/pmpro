---
description: 에스크로 결제 건에 대한 배송정보를 조회합니다.
---

# ⌨ 배송정보 단건조회 API

### 입력한 배송정보를 획득합니다.

<details>

<summary><strong>지원되는 PG사 확인하기</strong></summary>

* KG이니시스
* NHN KCP
* 페이조아(다우)

</details>

{% swagger method="get" path="/escrows/logis/{imp_uid}" baseUrl="https://api.iamport.kr" summary="등록한 배송정보를 단건 획득합니다." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="imp_uid" type="String" required="true" %}
<mark style="color:red;">

**아임포트 거래번호**

</mark>
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
{% tabs %}
{% tab title="EscrowLogisResponse" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`response`**<mark style="color:red;">**`(EscrowLogisAnnotation, optional)`**</mark>
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="EscrowLogisAnnotation" %}
**`company`  **<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**`택배사코드`**

&#x20;****&#x20;

**`invoice`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**`송장번호`**

&#x20;****&#x20;

**`sent_at`**<mark style="color:red;">**`*`**</mark><mark style="color:orange;">**`integer`**</mark>

**`발송일시`** _**UNIX TIMESTAMP**_

_****_

**`applied_at`**_<mark style="color:red;">**`*`**</mark>_<mark style="color:orange;">**`integer`**</mark>

**`배송정보 등록일시`** _**UNIX TIMESTAMP**_
{% endtab %}
{% endtabs %}
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="필수 파라메터가 누락되거나 (PG사별로 필수 여부가 다를 수 있음), 지원하는 않는 PG사인 경우" %}
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

{% swagger-response status="404: Not Found" description="배송정보를 조회할 거래건이 존재하지 않음" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="배송정보 조회 도중 오류 발생" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

<details>

<summary>Response Model Schema</summary>

```json
{
  "code": 0,
  "message": "string",
  "response": {
    "company": "string",
    "invoice": "string",
    "sent_at": 0,
    "applied_at": 0
  }
}
```

</details>

{% hint style="success" %}
**Swagger Test Link**

****[**https://api.iamport.kr/#!/escrow.logis/escrow\_logis\_get**](https://api.iamport.kr/#!/escrow.logis/escrow\_logis\_get)****
{% endhint %}

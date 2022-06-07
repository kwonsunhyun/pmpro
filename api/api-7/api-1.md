---
description: 배송정보를 등록할 수 있습니다.
---

# ⌨ 배송정보 단건등록 API

### 에스크로 거래 배송정보를 단건 등록합니다.

<details>

<summary><strong>지원되는 PG사 확인하기</strong></summary>

* KG이니시스

<!---->

* NHN KCP

<!---->

* 페이조아(다우)

</details>

{% swagger method="post" path="/escrows/logis/{imp_uid}" baseUrl="https://api.iamport.kr" summary="에스크로 거래 배송등록" %}
{% swagger-description %}
**2-depth**의 Json 으로 Request Body가 구성되어야 합니다

[**택배사 코드표**](../../tip/code.md)****
{% endswagger-description %}

{% swagger-parameter in="path" name="imp_uid" type="String" required="true" %}
<mark style="color:red;">

**아임포트 거래번호**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sender" type="Json" required="true" %}
<mark style="color:red;">

**발신자 정보**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="receiver" type="Json" required="true" %}
<mark style="color:red;">

**수신자 정보**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="logis" type="Json" required="true" %}
<mark style="color:red;">

**배송정보**

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

{% swagger-response status="404: Not Found" description="배송정보를 등록할 거래건이 존재하지 않음" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="405: Method Not Allowed" description="POST요청이 아닌 경우" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="409: Conflict" description="이미 배송정보 등록이 완료됨, 해당거래건은 배송정보를 등록할 수 없는경우" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="배송정보 등록 도중 오류 발생" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

### **주요 요청 파라미터 상세 설명**

> **`sender`**<mark style="color:red;">**`*`**</mark><mark style="color:blue;">**`Json`**</mark>
>
> **`발신자 정보`**

<details>

<summary>EscrowLogisSenderAnnotation</summary>

**`name (string, optional)`**

**`보내는분 성함(필수 : KG이니시스)`**&#x20;



**`tel (string, optional)`**

**`보내는분 전화번호(필수 : KG이니시스)`**



**`addr (string, optional)`**

**`보내는분 주소(필수 : KG이니시스)`**



**`postcode (string, optional)`**

**`보내는분 우편번호(필수 : KG이니시스)`**



**`relationship (string, optional)`**

**`보내는분과의 관계(필수 : 페이조아, 예: 본인)`**

</details>

> **`receiver`**<mark style="color:red;">**`*`**</mark><mark style="color:blue;">**`Json`**</mark>
>
> **`수신자 정보` **<mark style="color:blue;">****</mark>&#x20;

<details>

<summary>EscrowLogisReceiverAnnotation</summary>

**`name (string, optional)`**

**`받는 분 성함(필수 : KG이니시스)`**



**`tel (string, optional)`**&#x20;

**`받는 분 전화번호(필수 : KG이니시스)`**



**`addr (string, optional)`**

**`받는 분 주소(필수 : KG이니시스)`**



**`postcode (string, optional)`**

**`받는 분 우편번호(필수 : KG이니시스)`**

</details>

> **`logis`**<mark style="color:red;">**`*`**</mark><mark style="color:blue;">**`Json`**</mark>
>
> **`배송정보` **<mark style="color:blue;">****</mark>&#x20;

<details>

<summary>EscrowLogisInfoAnnotation</summary>

**`company (string)`**

**`택배사코드` **<mark style="color:blue;">****</mark>&#x20;



**`invoice (string)`**

**`송장번호`**



**`sent_at (integer)`**

**`발송일시 UNIX TIMESTAMP`**



**`receiving_at (string, optional)`**

**`수령일시(필수: 페이조아 / 예: YYYYMMDD)`**



**`address (string, optional)`**

**`발송주소(필수: 페이조아)`**

</details>

### 응답

<details>

<summary>Response Model Schema</summary>

```
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

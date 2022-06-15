---
description: 등록된 배송정보를 수정할 수 있습니다.
---

# ⌨ 배송정보 단건수정 API

### 등록한 배송정보를 단건 수정합니다.

<details>

<summary><strong>지원되는 PG사 확인하기</strong></summary>

* KG이니시스
* NHN KCP
* 페이조아(다우)

</details>

{% swagger method="put" path="/escrows/logis/{imp_uid}" baseUrl="https://api.iamport.kr" summary="배송정보 단건 수정" %}
{% swagger-description %}
에스크로 결제 건에 대해서 PUT /escrows/logis/{imp\_uid} 로 등록된 배송정보를 수정하는 API 입니다.

**2-depth**의 **Json**으로 **Request Body**가 구성되어야 합니다

logis는 하위 필드가 모두 필수입니다. sender, receiver의 각 세부 항목은 PG사마다 필수 여부가 모두 다릅니다.

수정시 수정할 항목과 기존 항목이 모두 기입되어야 합니다.
{% endswagger-description %}

{% swagger-parameter in="path" name="imp_uid" type="String" required="true" %}
<mark style="color:red;">

**아임포트 고유번호**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sender" type="json" required="true" %}
<mark style="color:red;">

**발신자 정보**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="receiver" type="json" required="true" %}
<mark style="color:red;">

**수신자 정보**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="logis" type="json" required="true" %}
<mark style="color:red;">

**배송정보**

</mark>
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
```javascript
{
    // Response
}
```
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

{% swagger-response status="404: Not Found" description="배송정보를 수정할 거래건이 존재하지 않음" %}
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

{% swagger-response status="409: Conflict" description="해당거래건은 배송정보를 수정할 수 없는 경우" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="배송정보 수정 도중 오류 발생" %}
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

**`name (`**<mark style="color:green;">**`string`**</mark>**`, optional)`**

**`보내는분 성함(필수 : KG이니시스)`**&#x20;



**`tel (`**<mark style="color:green;">**`string`**</mark>**`, optional)`**

**`보내는분 전화번호(필수 : KG이니시스)`**



**`addr (`**<mark style="color:green;">**`string`**</mark>**`, optional)`**

**`보내는분 주소(필수 : KG이니시스)`**



**`postcode (`**<mark style="color:green;">**`string`**</mark>**`, optional)`**

**`보내는분 우편번호(필수 : KG이니시스)`**



**`relationship (`**<mark style="color:green;">**`string`**</mark>**`, optional)`**

**`보내는분과의 관계(필수 : 페이조아, 예: 본인)`**

</details>

> **`receiver`**<mark style="color:red;">**`*`**</mark><mark style="color:blue;">**`Json`**</mark>
>
> **`수신자 정보` **<mark style="color:blue;">****</mark>&#x20;

<details>

<summary>EscrowLogisReceiverAnnotation</summary>

**`name (`**<mark style="color:green;">**`string`**</mark>**`, optional)`**

**`받는 분 성함(필수 : KG이니시스)`**



**`tel (`**<mark style="color:green;">**`string`**</mark>**`, optional)`**&#x20;

**`받는 분 전화번호(필수 : KG이니시스)`**



**`addr (`**<mark style="color:green;">**`string`**</mark>**`, optional)`**

**`받는 분 주소(필수 : KG이니시스)`**



**`postcode (`**<mark style="color:green;">**`string`**</mark>**`, optional)`**

**`받는 분 우편번호(필수 : KG이니시스)`**

</details>

> **`logis`**<mark style="color:red;">**`*`**</mark><mark style="color:blue;">**`Json`**</mark>
>
> **`배송정보` **<mark style="color:blue;">****</mark>&#x20;

<details>

<summary>EscrowLogisInfoAnnotation</summary>

**`company (`**<mark style="color:green;">**`string`**</mark>**`)`**

**`택배사코드` **<mark style="color:blue;">****</mark>&#x20;



**`invoice (`**<mark style="color:green;">**`string`**</mark>**`)`**

**`송장번호`**



**`sent_at (`**<mark style="color:purple;">**`integer`**</mark>**`)`**

**`발송일시 UNIX TIMESTAMP`**



**`receiving_at (string, optional)`**

**`수령일시(필수: 페이조아 / 예: YYYYMMDD)`**



**`address (`**<mark style="color:green;">**`string`**</mark>**`, optional)`**

**`발송주소(필수: 페이조아)`**

</details>

{% code title="요청 Body Sample" %}
```json
{
    "logis": {
        "invoice": "1728384716123",
        "company": "우체국",
        "receiving_at": "20220215",
        "address": "성수이로20길16"
    },
    "receiver": {
        "name": "홍길동"
    },
    "sender": {
        "relationship": "가족"
    }
}
```
{% endcode %}

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

****[**https://api.iamport.kr/#!/escrow.logis/escrow\_logis\_edit**](https://api.iamport.kr/#!/escrow.logis/escrow\_logis\_edit)****
{% endhint %}

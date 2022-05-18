---
description: 아임포트와 별개로 거래된 일반 현금결제에 대해서 발행된 현금영수증을 취소하는 API 입니다
---

# ⌨ 외부 발급분 취소 API

### 차이포트 별개거래로 발생된 현금영수증 거래를 취소합니다.

**지원되는 PG사**

<details>

<summary>확인하기</summary>

* **KG 이니시스**

<!---->

* **NHN KCP**

<!---->

* **Settle Bank**

<!---->

* **NICE Payments**

<!---->

* **PayJoa(다우)**

</details>

{% swagger method="delete" path="/receipts/external/{merchant_uid}" baseUrl="https://api.iamport.kr" summary="차이포트에서 발급하지 않은 PG발급 거래를 취소합니다." %}
{% swagger-description %}
차이포트와 별개로 거래된 일반 현금결제에 대해 차이포트 내에 설정된 PG사로 차이포트 API를 이용해 현금영수증을 발행취소하는 API입니다. 

**merchant_uid**

는 현금결제를 구분할 고유주문번호를 의미하며 발행에 사용된 값을 전달하면 됩니다.
{% endswagger-description %}

{% swagger-parameter in="path" name="merchant_uid" type="String" required="true" %}
<mark style="color:red;">**주문번호**</mark>** **&#x20;

발급취소대상 주문번호
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
{% tabs %}
{% tab title="ExternalReceiptResponse" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`response`**<mark style="color:red;">**`(ExternalReceiptAnnotation, optional)`**</mark>&#x20;
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="ExternalReceiptAnnotation" %}
**`merchant_uid`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**`주문번호`**



**`receipt_tid`` `**<mark style="color:green;">**`string`**</mark>

**`현금영수증 PG사 발행고유번호`**

&#x20;****&#x20;

**`apply_num`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>** **&#x20;

**`현금영수증 국세청 발행번호`**

&#x20;****&#x20;

**`type`` `**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**`현금영수증 발행대상 타입`**

* 개인 : `person` ****&#x20;
* 사업자 : `company`



**`amount`**<mark style="color:red;">**`*`**</mark><mark style="color:orange;">**`integer`**</mark>

**`현금영수증 발행금액`**

&#x20;****&#x20;

**`vat`**<mark style="color:red;">**`*`**</mark><mark style="color:orange;">**`integer`**</mark>

**`부가세`**

&#x20;****&#x20;

**`receipt_url`` `**<mark style="color:green;">**`string`**</mark>

**`발행된 현금영수증 URL` **&#x20;

****

**`applied_at`**<mark style="color:red;">**`*`**</mark><mark style="color:orange;">**`integer`**</mark>

**현금영수증 발행시각** `UNIX TIMESTAMP`

&#x20;

**`cancelled_at`` `**<mark style="color:orange;">**`integer`**</mark>

**`현금영수증 발행취소시각`** `UNIX TIMESTAMP`
{% endtab %}
{% endtabs %}
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="merchant_uid 파라메터가 누락된 경우" %}
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

{% swagger-response status="404: Not Found" description="현금영수증 발행된 적이 없는 merchant_uid 에 대해 요청한 경우" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="현금영수증 발행취소에 실패한 경우" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

### Response Model Schema

<details>

<summary>HTTP status 200</summary>

```
{
  "code": 0,
  "message": "string",
  "response": {
    "merchant_uid": "string",
    "receipt_tid": "string",
    "apply_num": "string",
    "type": "person",
    "amount": 0,
    "vat": 0,
    "receipt_url": "string",
    "applied_at": 0,
    "cancelled_at": 0
  }
}
```

</details>

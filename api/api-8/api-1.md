---
description: 처아포트를 통해 발행된 현금영수증 상세정보를 조회할 수 있습니다.
---

# ⌨ 발급내역 단건 조회 API

### 차이포트를 통해 발급된 현금영수증을 단건 조회 합니다.

{% swagger method="get" path="/receipts/{imp_uid}" baseUrl="https://api.iamport.kr" summary="현금영수증 단건조회 API" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="imp_uid" type="String" required="true" %}
<mark style="color:red;">

**차이포트 거래번호**

</mark>
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
{% tabs %}
{% tab title="ReceiptResponse" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`response`` `**<mark style="color:red;">**`(ReceiptAnnotation, optional)`**</mark>
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="ReceiptAnnotation" %}
**`imp_uid`` `**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**`차이포트 거래번호`**



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

{% swagger-response status="401: Unauthorized" description="인증 Token이 전달되지 않았거나 유효하지 않은 경우" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="존재하지 않는 차이포트 거래 정보이거나 현금영수증 발행된 내역이 확인되지 않는 경우" %}
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
    "imp_uid": "string",
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

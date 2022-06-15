---
description: 차이포트와 별개로 거래된 현금결제에 대한 현금영수증 발급을 진행할 수 있습니다.
---

# ⌨ 현금영수증 발급(외부) API

### 차이포트와 별개로 거래된 일반 현금결제에 대해서 현금영수증을 발행합니다.

<details>

<summary><strong>지원되는 PG사</strong> 확인하기</summary>

* **KG 이니시스**
* **NHN KCP**
* **Settle Bank**
* **NICE Payments**
* **페이조아(다우)**
* **KICC**

</details>

{% swagger method="post" path="/receipts/external/{merchant_uid}" baseUrl="https://api.iamport.kr" summary="현금영수증 발급 API" %}
{% swagger-description %}
차이포트 거래와 무관하게 현금영수증을 발급할수 있습니다. 단 주문번호는 현금거래 주문번호와 동일한 번호를 기재해야 추후 대사가 가능한점 유념하시기 바랍니다.

pg 파라메터를 지정하지 않으면, 기본 PG설정값을 이용해 발행시도하게 됩니다
{% endswagger-description %}

{% swagger-parameter in="path" name="merchant_uid" type="String" required="true" %}
<mark style="color:red;">

**주문번호**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="String" required="true" %}
<mark style="color:red;">

**현금영수증 발행 주문명**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="integer" required="true" %}
<mark style="color:red;">

**현금영수증 발행 금액**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="identifier" type="String" required="true" %}
<mark style="color:red;">**현금영수증 식별정보 구분코드**</mark>

`국세청현금영수증카드`

`휴대폰번호`

`주민등록번호`

`사업자등록번호`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="identifier_type" type="String" %}
**현금영수증 식별정보 구분코드**

`person : 주민등록번호`

`business : 사업자등록번호`

`phone : 휴대폰번호`

`taxcard : 국세청현금영수증카드`&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="String" %}
**현금영수증 발행 구분코드**&#x20;

`소득공제용(개인) : person`

`지출증빙용(법인) : company`&#x20;

`기본값 : person`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_name" type="String" %}
**구매자 이름 **

<mark style="color:red;">

****

</mark>

 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_email" type="String" %}
**구매자 Email**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_tel" type="String" %}
**구매자 전화번호**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tax_free" type="integer" %}
**면세금액**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pg" type="String" %}
**PG 구분코드**
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

{% swagger-response status="400: Bad Request" description="필수 파라메터가 누락된 경우, 이미 현금영수증 발행된 merchant_uid 에 대해 요청한 경우" %}
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

{% swagger-response status="500: Internal Server Error" description="현금영수증 발행에 실패한 경우" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

### **주요 요청 파라미터 상세 설명**

> **`identifier`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`String`**</mark>
>
> **`현금영수증 식별정보 구분코드` **<mark style="color:green;">****</mark>&#x20;
>
> 국세청현금영수증카드, 휴대폰번호, 주민등록번호, 사업자등록번호 를 기재합니다.

> **`identifier_type`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`String`**</mark>
>
> **`현금영수증 식별정보 구분코드` **&#x20;
>
> **KICC, 세틀뱅크**인 경우에만 <mark style="color:red;">**필수**</mark>
>
> KG이니시스/NHN KCP/나이스페이먼츠/페이조아는 **identifier 만으로 자동 처리**

> **`pg`    **<mark style="color:red;">**\***</mark>**    **<mark style="color:green;">**string**</mark>
>
> **pg 구분코드**
>
> 관리자콘솔 API 방식 비인증 PG설정이 2개 이상인 경우 필수적으로 기재해야 하는 항목입니다.
>
> 동일 PG사에 <mark style="color:red;">**두개의 MID**</mark> 를 설정한 경우 아래 양식으로 기재 합니다. ****&#x20;
>
> **{PG사}.{PG상점아이디}**
>
> 지정하지 않거나 유효하지 않은 값이 전달되면 기본PG설정된 값을 이용해 결제하게 됩니다.
>
> * 나이스페이먼츠, JTNet 2가지 PG설정이 되어있다면, pg 파라메터로 **nice** 또는 **jtnet**로 구분 가능
> * 나이스페이먼츠로부터 2개 이상의 상점아이디를 발급받았다면, **nice.MID1** 또는 **nice.MID2**로 구분 가능

<details>

<summary>Response Model Schema</summary>

```json
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

{% hint style="success" %}
**Swagger Test Link**

****[**https://api.iamport.kr/#!/receipts/issueExternalReceipt**](https://api.iamport.kr/#!/receipts/issueExternalReceipt)****
{% endhint %}

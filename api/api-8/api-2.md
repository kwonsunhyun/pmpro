---
description: 현금영수증을 발급할 수 있습니다.
---

# ⌨ 현금영수증 단건발급 API

### 현금영수증을 발급할 수 있습니다.

차이포트를 통해 발생된 현금성 거래(**가상계좌,게좌이체**)의 차이포트 거래번호(<mark style="color:red;">**`imp_uid`**</mark>)를 기준으로 현금영수증이 발급 됩니다. 현금영수증 발급 금액은 **현금성 거래의 금액으로 자동 적용**됩니다. 부분취소된 거래인 경우 **남은 잔액으로 발급**됩니다.

<details>

<summary><strong>지원되는 PG사</strong> 확인하기</summary>

* **KG 이니시스**
* **NHN KCP**
* **Settle Bank**
* **NICE Payments**
* **PayJoa(다우)**
* **KICC**

</details>

{% swagger method="post" path="/receipts/{imp_uid}" baseUrl="https://api.ianport.kr" summary="현금거래에 대한 현금영수증을 발급합니다." %}
{% swagger-description %}
현금영수증 발행을 처리하는 차이포트 API 입니다.
{% endswagger-description %}

{% swagger-parameter in="path" name="imp_uid" type="String" required="true" %}
<mark style="color:red;">

**차이포트 거래번호**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="identifier" type="String" required="true" %}
<mark style="color:red;">

**현금영수증 발행대상 식별정보**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="identifier_type" type="String" %}
**현금영수증 식별정보 구분코드**

`person : 주민등록번호`

`business : 사업자등록번호`

`phone : 휴대폰번호`

`taxcard : 국세청현금영수증카드`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="String" %}
**현금영수증 발행 구분코드**&#x20;

`소득공제용(개인) : person`

`지출증빙용(법인) : company`&#x20;

`기본값 : person`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="company_tel" type="String" %}
**발행 상점 고객센터 번호**

(페이조아인 경우만 필수)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="company_name" type="String" %}
**상점 사업자 명**

(페이조아인 경우만 필수)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="corp_reg_no" type="String" %}
**상점 사업자 번호**

(페이조아인 경우만 필수)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_name" type="String" %}
**구매자 이름**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_email" type="String" %}
**구매자 Email 주**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_tel" type="String" %}
**구매자 전화번호**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tax_free" type="integer" %}
**면세금액**
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

{% swagger-response status="400: Bad Request" description="필수 파라메터가 누락된 경우, 결제완료(paid)가 아닌 결제 건에 대해 발행요청한 경우, 이미 현금영수증 발행된 건에 대해 요청한 경우" %}
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

{% hint style="success" %}
**Swagger Test Link**

****[**https://api.iamport.kr/#!/receipts/issueReceipt**](https://api.iamport.kr/#!/receipts/issueReceipt)****
{% endhint %}

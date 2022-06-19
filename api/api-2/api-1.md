# ⌨ 빌링키 발급 API

### 카드정보를 이용하여 빌링키를 발급할수 있는 API 입니다.

{% swagger method="post" path="/subscribe/customer/{customer_uid}" baseUrl="https://api.iamport.kr" summary="빌링키 발급 API" %}
{% swagger-description %}
구매자에 대해 빌링키 발급을 요청 할 수 있습니다.
{% endswagger-description %}

{% swagger-parameter in="path" name="customer_uid" type="String(80)" required="true" %}
<mark style="color:red;">

**빌링키**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" required="true" name="pg" type="String" %}
**PG 구분코드**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="card_numb" type="String" required="true" %}
**카드번호**

<mark style="color:red;">**XXXX-XXXX-XXXX-XXXX**</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiry" type="String" required="true" %}
**카드 유효기간**

<mark style="color:red;">**YYYY-MM**</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="birth" type="String" required="false" %}
**생년월일 6자리**

**법인카드인 경우 사업자 번호 10자리**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pwd_2digit" type="String" required="false" %}
**카드비밀번호 앞 2자리**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cvc" type="String" required="false" %}
**카드 인증번호**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer_name" type="String" required="false" %}
**카드소유자명**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer_tel" type="String" required="false" %}
**카드소유자 연락처**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer_email" type="String" required="false" %}
**카드소유자 이메일주소**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer_addr" type="String" required="false" %}
**카드소유자 주소**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer_postcode" type="String" required="false" %}
카드소유자 우편번호
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer_id" type="String" %}
구매자 ID(

<mark style="color:red;">

**토스페이먼츠 전용**

</mark>

)
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="빌링키 발급성공" %}
{% tabs %}
{% tab title="CustomerResponse" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`response`** <mark style="color:red;">**(CustomerAnnotation, optional)**</mark>
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="CustomerAnnotation" %}
**`code`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:purple;">**integer**</mark>

**`응답코드`**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**`응답메세지`**

code값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`customer_uid`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**`고객 고유번호`**\
****

**`pg_provider`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**빌링키가 등록된 PG사 코드**

****

**`pg_id`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**빌링키가 등록된 PG사 상점아이디(MID)**

****

**`card_name`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**`카드사명`**

****

**`card_code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`카드사 코드`**

&#x20;****&#x20;

**`card_number`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`마스킹 카드번호`**

****

**`card_type`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`카드유형`**

**(주의)해당 정보를 제공하지 않는 일부 PG사의 경우 null 로 응답됨**

****

**`customer_name`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`고객성함`**

****

**`customer_tel`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**`고객 전화번호`**

****

**`customer_email`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`고객 Email`**

****

**`customer_addr`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`고객 주소` **&#x20;

&#x20;

**`customer_postcode`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`고객 우편번호`**



**`inserted`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**`빌키가 등록된 시각`** UNIX timestamp



**`updated`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**`빌키가 업데이트된 시각`** UNIX timestamp
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
{% endswagger %}

### **주요 요청 파라미터 상세 설명**

> **`pg`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>
>
> **PG 구분코드**
>
> 한 PG사에 복수개 MID 를 이용중인 경우 <mark style="color:red;">**PG구분코드.MID**</mark> 형태로 기입하시면 됩니다.
>
> _ex) NHN KCP를 사용하고 사이트 코드가 IPXC 인 경우_
>
> **kcp.IPXC**

> **`birth`** <mark style="color:red;">\*</mark> <mark style="color:green;">**string**</mark>
>
> **생년월일**
>
> 일부 PG사에 한하여 생략 가능(PG사 협의 필요)

> **`customer_id`` `**<mark style="color:green;">**`string`**</mark>
>
> **`구매자 ID` **<mark style="color:green;">****</mark>&#x20;
>
> 빌링키를 발급한 고객의 고유 ID <mark style="color:green;">****</mark>** **<mark style="color:red;">**토스페이먼츠 전용**</mark>** **<mark style="color:green;">****</mark>&#x20;

{% hint style="info" %}
**해당 빌링키 발급 API 는 PG사와 협의가 완료된 경우 이용 가능한 서비스입니다.**

* PG사 협의를 통해 카드정보 필수 조건 값 조정이 가능합니다.
* 민감한 카드정보를 이용하기 때문에 보안에 특히 유의하셔야 합니다.
* customer\_uid 값은 **고객 & 카드번호** 단위별로 고유하게 발급 관리되어야 합니다
{% endhint %}

<details>

<summary>Response Model Schema</summary>

```json
{
  "code": 0,
  "message": "string",
  "response": {
    "customer_uid": "string",
    "pg_provider": "string",
    "pg_id": "string",
    "card_name": "string",
    "card_code": "string",
    "card_number": "string",
    "card_type": "null",
    "customer_name": "string",
    "customer_tel": "string",
    "customer_email": "string",
    "customer_addr": "string",
    "customer_postcode": "string",
    "inserted": 0,
    "updated": 0
  }
```

</details>

{% hint style="success" %}
**Swagger Test Link**

****[**https://api.iamport.kr/#!/subscribe.customer/customer\_save**](https://api.iamport.kr/#!/subscribe.customer/customer\_save)****
{% endhint %}

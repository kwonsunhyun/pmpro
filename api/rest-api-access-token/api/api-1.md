---
description: 카드정보를 기입하여 1회성 결제를 요청할 수 있습니다.
---

# ⌨ 비 인증 결제(일회성) API

### 카드정보만으로 결제를 요청할 수 있습니다.

{% swagger method="post" path="/onetime" baseUrl="https://api.iamport.kr/subscribe/payments" summary="구매자로부터 별도의 인증과정을 거치지 않고 카드정보만으로 결제를 진행하는 API 입니다." %}
{% swagger-description %}
**customer_uid**

 를 전달해주시면 결제 후 다음 번 결제를 위해 성공된 결제에 사용된 빌링키를 저장해두게되고 customer_uid가 없는 경우 저장되지 않습니다. 동일한 

**merchant_uid는 재사용이 불가**

능하며 고유한 값을 전달해주셔야 합니다.
{% endswagger-description %}

{% swagger-parameter in="body" name="merchant_uid" type="String" required="true" %}
<mark style="color:red;">

**주문번호**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="currency" %}
결제통화 구분코드

KRW, USD, VND ...
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="double" required="true" %}
<mark style="color:red;">

**결제금액**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tax_free" type="double" %}
면세금액
{% endswagger-parameter %}

{% swagger-parameter in="body" name="card_number" type="String" required="true" %}
<mark style="color:red;">**카드번호**</mark>

**(dddd-dddd-dddd-dddd)**

<mark style="color:red;">****</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiry" type="String" required="true" %}
<mark style="color:red;">**카드 유효기간**</mark>

**(YYYY-MM)**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="birth" type="String" required="true" %}
<mark style="color:red;">**생년월일 6자리**</mark>** (yymmdd)**

(법인카드의 경우 사업자등록번호10자리)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pwd_2digit" type="String" %}
카드비밀번호 앞 2자리
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cvc" type="String" %}
카드 인증번호&#x20;

(카드 뒷면 3자리, AMEX의 경우 4자리). **Paymentwall 에서만 사용**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer_uid" type="String" %}
결제에 사용된 카드정보를 빌링키 형태로 저장해두고 재 결제에 사용하시려면 customer_uid를 지정해주세요
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pg" type="String" required="true" %}
<mark style="color:red;">

**pg 구분코드**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="String" %}
제품명
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_name" type="String" %}
구매자명
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_email" type="String" %}
주문자 E-mail주소
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_tel" type="String" %}
주문자 전화번호
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_addr" type="String" %}
주문자 주소
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_postcode" type="String" %}
주문자 우편번호
{% endswagger-parameter %}

{% swagger-parameter in="body" name="card_quota" type="integer" %}
카드할부개월수
{% endswagger-parameter %}

{% swagger-parameter in="body" name="interest_free_by_merchant" type="boolen" %}
가맹점부담 무이자 할부여부
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_data" type="String" %}
에코항목
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notice_url" type="String" %}
결제성공 시 통지될 웹훅 URL
{% endswagger-parameter %}

{% swagger-parameter in="body" name="browser_ip" type="String" %}
매자 브라우져(PC)의 IP
{% endswagger-parameter %}

{% swagger-parameter in="body" name="secure_3d_charge_id" type="String" %}
(해외PG 전용) 3D secure 인증 후 재결제시 PG사에서 부여한 결제 ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="secure_3d_token" type="String" %}
(해외PG 전용) 3D secure 인증 후 재결제시 PG사에서 부여한 토큰
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="결제 성공" %}
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
{% endswagger %}

---
description: 결제 URL 생성 API 명세를 기술합니다.
---

# 💻 결제 URL 생성하기

### 1. 개요

본 문서는 아임포트에서 제공하는 결제 URL 생성 API 명세를 기술합니다. 아임포트 서비스를 이용중인 가맹점은 해당 서비스를 제약없이 이용 가능합니다.

### 2. API URI

해당 API는 REST 방식으로 구현되어 인터넷 웹 서비스의 형태로 제공됩니다.

> **HTTP Method : POST**
>
> **Content-Type : Application.json;charset=UTF-8**

{% tabs %}
{% tab title="개발" %}
{% code title="URI" %}
```url
https://api.iamport-dev.co/api/supplements/v1/link/payment
```
{% endcode %}
{% endtab %}

{% tab title="운영" %}
{% code title="URI" %}
```
https://api.iamport.co/api/supplements/v1/link/payment
```
{% endcode %}
{% endtab %}
{% endtabs %}

### 3. 설명

결제가 가능한 URL을 생성하여 고객이 해당 URL에 접근하 결제를 진행 할 수 있습니다. PG사가 지원하는 모든 결제수단 지원이 가능하며 설정한 시간이 만료된 경우 해당 URL 접근시 결제를 진행할 수 없습니다.

### 4. 요청 메세시 상세

{% swagger method="post" path="/payment" baseUrl="https://api.iamport.co/api/supplements/v1/link" summary="결제URL을 생성합니다." %}
{% swagger-description %}
HTTP Method : POST

Content-Type : Application.<mark style="color:red;">json</mark>;charset=UTF-8
{% endswagger-description %}

{% swagger-parameter in="body" name="title" type="String" required="true" %}
<mark style="color:red;">

브릿지 페이지 노출문구

</mark>

 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user_code" type="String" required="true" %}
<mark style="color:red;">

가맹점식별코드

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="integer" required="true" %}
<mark style="color:red;">

결제금액

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="merchant_uid" type="String" required="true" %}
<mark style="color:red;">

주문번호

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="String" required="true" %}
<mark style="color:red;">

제품명

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tax_free" type="integer" required="false" %}
면세금액
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="String" required="true" %}
<mark style="color:red;">

통화구분코드

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="language" type="String" required="false" %}
실 결제창 표기언어

\-ko

\-en
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_name" type="String" required="false" %}
주문자명
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_tel" type="String" required="true" %}
<mark style="color:red;">

주문자연락처

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_addr" type="String" required="false" %}
주문자주소
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_email" type="String" required="false" %}
주문자 이메일주
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_postcode" type="String" required="false" %}
주문자 우편번호
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_data" type="Object" required="false" %}
에코항목
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notice_url" type="String" required="false" %}
결제결과를 수신받을 URL
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expire_at" type="String" required="true" %}
<mark style="color:red;">

페이지 만료시각

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="display_language" type="String" required="false" %}
브릿지 페이지 표기언어

\-ko : 한국어

\-en : 영어
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pay_methods" type="Object" required="true" %}
**pg  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

pg사 구분코드

[#undefined](../sdk/javascript-sdk/undefined.md#undefined "mention")

***

**pay\_method **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

결제수단 구분코드

[#undefined](../sdk/javascript-sdk/undefined.md#undefined "mention")

***

**label  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

브릿지페이지 결제수단 표현값
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
{% code title="json" %}
```json
{
    "shortenedUrl": "https://dev.impay.link/4bdf239e"  //결제링크 생성 
}
```
{% endcode %}
{% endswagger-response %}
{% endswagger %}

**#요청 JSON 전문 예시**

{% code title="json" %}
```
{
    "payment_info": "{\"title\":\"테스트가맹점\",\"user_code\":\"imp68124833\",\"amount\":10000,\"merchant_uid\":\"merchant_1630665784552\",\"name\":\"결제링크 테스트\",\"tax_free\":\"면세공급가액\",\"currency\":\"KRW\",\"language\":\"ko\",\"buyer_name\":\"\",\"buyer_tel\":\"\",\"buyer_addr\":\"\",\"buyer_email\":\"\",\"buyer_postcode\":\"\",\"custom_data\":\"json_object\",\"notice_url\":\"결제 결과를 받을 url\",\"pay_methods\":[{\"pg\":\"INIpayTest\",\"pay_method\":\"card\",\"label\":\"신용/체크카드\"},{\"pg\":\"INIpayTest\",\"pay_method\":\"naverpay\",\"label\":\"네이버페이\"},{\"pg\":\"INIpayTest\",\"pay_method\":\"kakaopay\",\"label\":\"카카오페이\"},{\"pg\":\"INIpayTest\",\"pay_method\":\"phone\",\"label\":\"핸드폰 소액결제\"},{\"pg\":\"INIpayTest\",\"pay_method\":\"trans\",\"label\":\"계좌이체\"},{\"pg\":\"INIpayTest\",\"pay_method\":\"vbank\",\"label\":\"가상계좌\"}]}",
    "expired_at": 1634324016
}
```
{% endcode %}

**#결제(브릿지) 페이지 화면 예시**

{% tabs %}
{% tab title="결제(브릿지) 페이지" %}
**결제 URL API 요청이 성공한경우 응답 URL 렌더링 화면 예시입니다.**

![결제 URL 페이지 화면](<../.gitbook/assets/image (6).png>)
{% endtab %}

{% tab title=" 만료(브릿지) 화면" %}
**결제 URL 페이지 만료시각(expire\_at)이 지난 경우 표시되는 화면입니다.**

![결제 URL만료 화면](<../.gitbook/assets/image (4).png>)
{% endtab %}
{% endtabs %}

### 5.결제 URL 비활성화 방법

**응답**(**shortenedUrl**) **URL 마지막 String 을 결제 URI API 주소 뒤에 삽입하여 호출**

> **HTTP Method : **<mark style="color:red;">**PUT**</mark>

{% hint style="success" %}
**API 응답이 아래와 같은경우**

{

&#x20;       "**shortenedUrl**": "[https://dev.impay.link/<mark style="color:red;">**4bdf239e**</mark>](https://dev.impay.link/\*\*4bdf239e\*\*)"

}

[https://api.iamport.co/api/supplements/v1/link/payment/](https://api.iamport.co/api/supplements/v1/link/payment/%7BGUID%7D)<mark style="color:red;">**4bdf239e**</mark>

위와 같이 호출시 결제 URL 즉시 비활성화 처리됩니다.
{% endhint %}

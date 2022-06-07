---
description: 스마트로 결제창 연동 방법을 안내합니다.
---

# ⌨ 스마트로

### 1. 스마트로 PG 설정하기

****[**스마트로 설정**](../../ready/2.-pg/payment-gateway/undefined-5.md) **** 페이지의 내용을 참고하여 PG 설정을 진행합니다.

![](<../../.gitbook/assets/스크린샷 2022-06-03 오전 10.04.02.png>)

### 2.결제 요청하기

[JavaScript SDK](../../sdk/javascript-sdk/) IMP.**request\_pay**(param, callback)을 호출하여 스마트로 결제창을 호출할 수 있습니다. **결제결과**는 PC의 경우 IMP.request\_pay(param, callback) 호출 후 <mark style="color:red;">**callback**</mark>으로 수신되고 모바일의 경우 <mark style="color:red;">**m\_redirect\_url**</mark>** ** 로 리디렉션됩니다.

{% tabs %}
{% tab title="인증결제창 요청" %}
{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
    pg : 'smartro',
    pay_method : 'card',
    merchant_uid: "order_no_0001", //상점에서 생성한 고유 주문번호
    name : '주문명:결제테스트',
    amount : 1004,
    buyer_email : 'iamport@siot.do',
    buyer_name : '구매자이름',
    buyer_tel : '010-1234-5678',
    buyer_addr : '서울특별시 강남구 삼성동',
    buyer_postcode : '123-456',
    m_redirect_url : '{모바일에서 결제 완료 후 리디렉션 될 URL}' 
}, function(rsp) { // callback 로직
	//* ...중략... *//
});
```
{% endcode %}

####

### 주요 파라미터 설명

**`pg`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**PG사 구분코드**

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 **`smartro`** 로 지정하셔야 합니다.



**`pay_method`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**결제수단 구분코드**

* card (신용카드)
* trans (실시간 계좌이체)
* vbank(가상계좌)



**`merchant_uid`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**`주문번호`**

매번 고유하게 채번되어야 합니다.



**`amount`**<mark style="color:red;">**`*`**</mark><mark style="color:purple;">**`integer`**</mark>

**결제금액**

<mark style="color:green;">**string**</mark> 이 아닌점에 유의하세요
{% endtab %}
{% endtabs %}

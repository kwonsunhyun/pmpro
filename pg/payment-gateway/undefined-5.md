---
description: 페이팔 결제연동 방법을 안내합니다.
---

# ⌨ 페이팔

### 1. 페이팔 PG 설정하기

****[**페이팔 설정**](../../undefined/2.-pg/payment-gateway/undefined-6.md) **** 페이지의 내용을 참고하여 PG 설정을 진행합니다.

![](<../../.gitbook/assets/스크린샷 2022-06-03 오후 1.01.05.png>)



### 2.결제 요청하기

[JavaScript SDK](../../sdk/javascript-sdk/) IMP.**request\_pay**(param, callback)을 호출하여 스마트로 결제창을 호출할 수 있습니다. **결제결과**는 **PC / 모바일** 모두  <mark style="color:red;">**m\_redirect\_url**</mark> 리디렉션됩니다.

{% tabs %}
{% tab title="인증결제창 요청" %}
{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
    pg : 'paypal',
    pay_method : 'card',
    merchant_uid: "order_no_0001", // 상점에서 관리하는 주문 번호
    name : '주문명:결제테스트',
    amount : 14.20,
    currency : 'USD', // 기본값: USD(원화 KRW는 페이팔 정책으로 인해 지원하지 않음)
    buyer_email : 'iamport@siot.do',
    buyer_name : '구매자이름',
    buyer_tel : '010-1234-5678',
    buyer_addr : '서울특별시 강남구 삼성동',
    buyer_postcode : '123-456',
    m_redirect_url : '{결제 완료 후 리디렉션 될 URL}' 
}, function(rsp) { // callback 로직
	//* ...중략... *//
});
```
{% endcode %}

####

### 주요 파라미터 설명

**`pg`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**PG사 구분코드**

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 **`paypal`** 로 지정하셔야 합니다.



**`pay_method`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**결제수단 구분코드**

* card (신용카드)



**`merchant_uid`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**`주문번호`**

매번 고유하게 채번되어야 합니다.



**`amount`**<mark style="color:red;">**`*`**</mark><mark style="color:purple;">**`integer`**</mark>

**결제금액**

<mark style="color:green;">**string**</mark> 이 아닌점에 유의하세요



**`currency`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**결제통화코드 **<mark style="color:green;">****</mark>&#x20;

지원 가능한 모든 통화는 [페이팔 공식 문서](https://developer.paypal.com/docs/api/reference/currency-codes/#paypal-account-payments)를 참고해주세요



**`m_redirect_url`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**결제결과 수신 URL **<mark style="color:green;">****</mark>&#x20;

PC환경 모바일 환경 모두 해당 값을 필수로 설정해야 결과를 받아볼수 있습니다.
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
### 참고사항

아임포트는 페이팔 정기결제를 지원하지 않습니다.
{% endhint %}

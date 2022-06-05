---
description: 토스 간편결제 연동 방법을 안내합니다.
---

# ⌨ 토스 간편결제

### 1. 토스 간편결제 설정하기

****[**토스 간편결제 설정**](<../../undefined/2.-pg/pg/undefined-2 (1).md>) 페이지의 내용을 참고하여 PG 설정을 진행합니다.

![](<../../.gitbook/assets/스크린샷 2022-06-05 오후 1.29.25.png>)

### 2.결제 요청하기

[JavaScript SDK](../../sdk/javascript-sdk/) IMP.**request\_pay**(param, callback)을 호출하여 토스간편결제 결제창을 호출할 수 있습니다. **결제결과**는 PC의 / 모바일 모두 <mark style="color:red;">**m\_redirect\_url**</mark>** ** 로 리디렉션됩니다.

{% tabs %}
{% tab title="일반결제창 요청" %}
{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
    pg : 'tosspay',
    pay_method : 'card',
    merchant_uid: "order_no_0001", //상점에서 생성한 고유 주문번호
    name : '주문명:결제테스트',   //필수 파라미터 입니다.
    amount : 1004,
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

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 **`tosspay`** 로 지정해야 합니다.



**`pay_method`** <mark style="color:red;">****</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**결제수단 구분코드**

신용카드 : `card` | 계좌이체 : `trans`



**`name`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**제품명 **<mark style="color:green;">****</mark>&#x20;



**`merchant_uid`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**주문번호**

매번 고유하게 채번되어야 합니다.



**`amount`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**결제금액**

<mark style="color:green;">**string**</mark> 이 아닌점에 유의하세요



{% embed url="https://codepen.io/chaiport/pen/wvyxzYv" %}
**토스 간편결제 결제창 예시**
{% endembed %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**토스페이 간편결제는 스마트폰 토스 앱상에서 결제가 진행됩니다.**
{% endhint %}

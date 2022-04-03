---
description: NHN KCP 인증결제 연동 가이드입니다.
---

# ⌨ NHH KCP

### 1. PG 설정하기

[NHN KCP 일반결제 테스트 모드 설정](../undefined/2.-pg/nhn-kcp.md) 페이지의 내용을 참고하여 PG 설정을 합니다.

### 2.결제창 요청하기

[JavaScript SDK](../sdk/javascript-sdk/) IMP.**request\_pay**(param, callback)을 호출하여 NHN KCP 결제창을 호출할 수 있습니다.&#x20;

**결제결과**는 PC의 경우 IMP.request\_pay(param, callback) 호출 후 **callback**으로 실행되고, 모바일의 경우 **m\_redirect\_url**로 리디렉션됩니다.

{% tabs %}
{% tab title="인증결제 호출하기" %}
{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
    pg : 'kcp',
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

###

### 주요 파라미터 설명

**`pg`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**String**</mark>

**PG사 구분코드**

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 `kcp`로 지정하셔야 합니다.



**`pay_method`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**String**</mark>

**결제수단 구분코드**

* &#x20;card(신용카드)&#x20;
* samsung(삼성페이)
* trans(실시간 계좌이체)
* vbank(가상계좌)
* phone(휴대폰소액결제)
* payco(페이코 허브형)&#x20;
* naverpay(네이버페이)



**`merchant_uid`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**String**</mark>

**주문번호**

매번 고유하게 채번되어야 합니다.



**`amount` **<mark style="color:green;">****</mark>** **<mark style="color:red;">**\***</mark>** **<mark style="color:orange;">**integer**</mark>

**결제금액**

String **** 이 아닌점에 유의하세요



{% hint style="info" %}
**payco 허브형**인 경우 KCP 관리자페이지 신청 및 설정이 필요합니다.

신청안내 링크 : [https://sir.kr/main/service/p\_payco\_hub.php](https://sir.kr/main/service/p\_payco\_hub.php)
{% endhint %}

{% embed url="https://codepen.io/chaiport/pen/NWXrGvQ" %}
{% endtab %}

{% tab title="비 인증결제 호출하기" %}

{% endtab %}
{% endtabs %}

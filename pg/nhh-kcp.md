---
description: NHN KCP 결제창 연동 가이드입니다.
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
인증결제창 호출 파라미터에서 **customer\_uid** 값을 추가하면 비 인증 결제창을 호출할 수 있습니다. 비인증 결제창에서 빌링키를 발급받은 후 해당 빌링키로 결제를 요청합니다.

{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
    pg : 'kcp_billing',
    pay_method : 'card', // 'card'만 지원됩니다.
    merchant_uid: "order_monthly_0001", // 상점에서 관리하는 주문 번호
    name : '최초인증결제',
    amount : 0, // 결제창에 표시될 금액. 실제 승인이 이뤄지지는 않습니다. (PC에서는 가격이 표시되지 않음)
    customer_uid : 'your-customer-unique-id', // 필수 입력.
    buyer_email : 'iamport@siot.do',
    buyer_name : '아임포트',
    buyer_tel : '02-1234-1234',
    m_redirect_url : '{모바일에서 결제 완료 후 리디렉션 될 URL}' 
}, function(rsp) {
	if ( rsp.success ) {
		alert('빌링키 발급 성공');
	} else {
		alert('빌링키 발급 실패');
	}
});
```
{% endcode %}

{% hint style="success" %}
비인증 결제를 위해서는 KCP와 협의가 완료된 사이트코드를 관리자콘솔에 설정하셔야 비인증 결제창을 활성화 시킬수 있습니다.
{% endhint %}

###

### 주요 파라미터 설명

**`pg`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**String**</mark>

**PG사 구분코드**

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 `kcp_billing`으로 지정합니다.



**`customer_uid`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**String**</mark>

**카드 빌링키**

비 인증 결제창에서 고객이 입력한 카드정보와 1:1로 매칭될 빌링키를 지정합니다.



**`amount` **<mark style="color:green;">****</mark>** **<mark style="color:red;">**\***</mark>** **<mark style="color:orange;">**Integer**</mark>

**결제금액**

결제창에 표시될 금액으로 <mark style="color:red;">실제 승인은 이루어지지 않습니다.</mark>(실 결제를 발생시키기 위해서는 **customer\_uid** 로 **REST API 를 이용하여 결제요청**을 해주셔야 합니다.)



### 빌링키(customer\_uid)로 결제 요청하기
{% endtab %}
{% endtabs %}








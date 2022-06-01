---
description: JTNET 결제 연동 방법을 안내합니다.
---

# ⌨ JTNET

### 1. JTNET PG 설정하기

****[**JTNET 설정**](../undefined/2.-pg/pg/jtnet.md) **** 페이지의 내용을 참고하여 PG 설정을 진행합니다.

![](<../.gitbook/assets/스크린샷 2022-05-31 오후 12.07.01.png>)

### 2.결제창 요청하기

[JavaScript SDK](../sdk/javascript-sdk/) IMP.**request\_pay**(param, callback)을 호출하여 JTNET 결제창을 호출할 수 있습니다. **결제결과**는 PC의 경우 IMP.request\_pay(param, callback) 호출 후 **callback**으로 수신되 모바일의 경우 **m\_redirect\_url**로 리디렉션됩니다.

{% tabs %}
{% tab title="인증결제창 요청" %}
{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
    pg : 'jtnet',
    pay_method : 'card',
    merchant_uid: "order_no_0001", //상점에서 생성한 고유 주문번호
    name : '주문명:결제테스트',
    amount : 14000,
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

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 **`jtnet`** 로 지정하셔야 합니다.



**`pay_method`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**결제수단 구분코드**

* card (신용카드)
* trans (실시간 계좌이체)
* vbank(가상계좌)
* phone (휴대폰소액결제)



**`merchant_uid`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**`주문번호`**

매번 고유하게 채번되어야 합니다.



**`amount`**<mark style="color:red;">**`*`**</mark><mark style="color:purple;">**`integer`**</mark>

**결제금액**

<mark style="color:green;">**string**</mark> 이 아닌점에 유의하세요



{% embed url="https://codepen.io/chaiport/pen/qBxoPoN" %}
**인증결제창 예시**
{% endembed %}
{% endtab %}

{% tab title="비인증 결제창 요청" %}
인증결제창 호출 파라미터에서 **customer\_uid** 값을 추가하면 비 인증 결제창을 호출할 수 있습니다.   &#x20;



{% hint style="danger" %}
#### **amount 금액**

* 빌링키 발급시 amount 파라미터에 <mark style="color:red;">**금액이 설정되는 경우**</mark> **실 결제와 동시에 빌링키가 발급**됩니다.
* 실결제를 원하지 않은 경우 amount 금액을 <mark style="color:red;">**0원**</mark>으로 설정합니다.
{% endhint %}



{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
   pg : 'jtnet',
   pay_method : 'card', // 'card'만 지원됩니다.
   merchant_uid: "order_monthly_0001", // 상점에서 관리하는 주문 번호
   name : '최초인증결제',
   amount : 0, // 빌링키 발급만 진행하며 결제승인을 하지 않습니다.
   customer_uid : 'your-customer-unique-id', // 필수 입력
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



### 주요 파라미터 설명

**`pg`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**PG사 구분코드**

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 **`jtnet`** 으로 지정합니다.\


**`customer_uid`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**카드 빌링키**

비 인증 결제창에서 고객이 입력한 카드정보와 1:1로 매칭될 빌링키를 지정합니다.



**`amount`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**Integer**</mark>

**결제금액**

0원으로 설정시 빌링키만 발급되며 0원 이상 설정시 **실 결제와 빌링키 발급이 동시**에 이루어 집니다.\


### 빌링키(customer\_uid)로 결제 요청하기

빌링키 발급이 성공하면 실 빌링키는 customer\_uid 와 1:1 매칭되어 **아임포트 서버에 저장**됩니다. customer\_uid를 가맹점 내부서버에 저장하시고 [<mark style="color:blue;">**비 인증 결제요청 REST API**</mark>](../api/api-4/api.md)를 호출하시면 결제를 발생시킬 수 있습니다.



{% code title="sever-side" %}
```
curl -H "Content-Type: application/json" \   
     -X POST -d '{"customer_uid":"your-customer-unique-id", "merchant_uid":"order_id_8237352", "amount":3000}' \
     https://api.iamport.kr/subscribe/payments/again
```
{% endcode %}

**API 방식으로 빌링키 발급,결제요청,예약결제를 구현할수 있습니다. 자세한 가이드는 아래 링크를 참조하세요**

{% content-ref url="../undefined-1/undefined-1/" %}
[undefined-1](../undefined-1/undefined-1/)
{% endcontent-ref %}
{% endtab %}

{% tab title="비인증 API  결제요청" %}
### **API 방식으로 빌링키 발급,결제요청,예약결제를 구현할수 있습니다.**

### 일회성 결제 요청하기

REST[ **API POST /subscribe/payments/onetime**](../api/api-4/api-1.md)을 호출하여 일회성 결제를 요청합니다. 요청 시 전달된 카드는 아임포트에 등록되지 않습니다.

```
curl -H "Content-Type: application/json" \   
     -X POST -d '{"merchant_uid":"order_id_8237352", "card_number":"1234-1234-1234-1234", "expiry":"2019-01", "birth":"123456", "amount":3000}' \
     https://api.iamport.kr/subscribe/payments/onetime
```

###

### 빌링키 발급 요청하기

REST [**API POST /subscribe/customers/{customer\_uid}**](../api/api-2/api-1.md)를 호출하여 빌링키 발급을 요청합니다.

```
curl -H "Content-Type: application/json" \   
     -X POST -d '{"card_number":"1234-1234-1234-1234", "expiry":"2025-12", "birth":"820213", "pwd_2digit":"00"}' \
     https://api.iamport.kr/subscribe/customers/your-customer-unique-id
```

###

### 빌링키 발급 및 최초 결제 요청하기

REST [**API POST /subscribe/payments/onetime**](../api/api-4/api-1.md)을 호출하여 빌링키 발급과 최초 결제를 요청합니다.

* **`customer_uid`** : 빌링키 등록을 위해서 지정해야 합니다.

```
curl -H "Content-Type: application/json" \   
     -X POST -d '{"customer_uid":"your-customer-unique-id", "merchant_uid":"order_id_8237352", "card_number":"1234-1234-1234-1234", "expiry":"2019-01", "birth":"123456", "amount":3000}' \
     https://api.iamport.kr/subscribe/payments/onetime 
```

###

### 빌링키로 결제 요청하기

빌링키 발급과 최초 결제가 성공하면 빌링키는 전달된 `customer_uid` 와 1:1 매칭되어 아임포트에 저장됩니다. 보안상의 이유로 서버는 빌링키에 직접 접근할 수 없기 때문에 `customer_uid`를 이용해서 재결제([**POST /subscribe/payments/again**](../api/api-4/api.md)) REST API를 다음과 같이 호출합니다.

```
curl -H "Content-Type: application/json" \   
     -X POST -d '{"customer_uid":"your-customer-unique-id", "merchant_uid":"order_id_8237352", "amount":3000}' \
     https://api.iamport.kr/subscribe/payments/again
```

****

**자세한 가이드는 아래 링크를 참조하세요**

{% content-ref url="../undefined-1/undefined-1/" %}
[undefined-1](../undefined-1/undefined-1/)
{% endcontent-ref %}
{% endtab %}
{% endtabs %}

### ****3. 부가기능

{% tabs %}
{% tab title="특정 카드사 노출" %}
{% code title="javascript" %}
```javascript
card : {
    detail : [
        {card_code:"*", enabled:false},     //모든 카드사 비활성화
        {card_code:'366', enabled:true}     //특정 카드만 활성화
    ]
}
```
{% endcode %}



**파라미터 설명**

* **card\_code :** 금결원 카드사코드 [<mark style="color:red;">**링크**</mark>](https://chaifinance.notion.site/53589280bbc94fab938d93257d452216?v=eb405baf52134b3f90d438e3bf763630) 참조 (<mark style="color:green;">**string)**</mark>
* **enabled :** 해당카드 활성화 여부 (<mark style="color:orange;">**boolean)**</mark>
{% endtab %}
{% endtabs %}

---
description: 다우 연동 방법을 안내합니다.
---

# ⌨ 다우(페이조아)

### 1. 다 PG 설정하기

****[**다우 설정**](../../undefined/2.-pg/pg/undefined-2.md) 페이지의 내용을 참고하여 PG 설정을 진행합니다.

![](<../../.gitbook/assets/스크린샷 2022-06-05 오전 11.53.10.png>)

### 2.결제 요청하기

[JavaScript SDK](../../sdk/javascript-sdk/) IMP.**request\_pay**(param, callback)을 호출하여 다우 페이조아 결제창을 호출할 수 있습니다. **결제결과**는 PC의 경우 IMP.request\_pay(param, callback) 호출 후 <mark style="color:red;">**callback**</mark>** ** 으로 수신되고 모바일의 경우<mark style="color:red;">**m\_redirect\_url**</mark>** ** 로 리디렉션됩니다.

{% hint style="warning" %}
**페이조아 결제창 연동을 위해서는 **<mark style="color:red;">**JS SDK Version 1.2.0**</mark>** 이상을 사용하셔야 합니다.**
{% endhint %}

{% tabs %}
{% tab title="인증결제창 요청" %}
{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
    pg: 'daou',
    pay_method: 'card',
    merchant_uid: 'mid_1234567890',
    escrow: false,
    digital: false,
    amount: 1004,
    name: '노스페이스 롱패딩 M',
    buyer_name: '홍길동',
    buyer_email: 'hello@world.com',
    buyer_tel: '01012345678',
    digital : false, // 디지털로 계약되었다면 true로 설정
    m_redirect_url: 'https://allerts.com/payments/complete', 
    bypass: {
	// 페이조아(다우데이타) 전용 파라미터
        daou: {
	    PRODUCTCODE: 'iamport',
	    CASHRECEIPTFLAG: 2,
	},
    },
    app_scheme: 'iamportappscheme',
}, function(rsp) { // callback 로직
	//* ...중략... *//
});
```
{% endcode %}

####

### 주요 파라미터 설명

**`pg`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**PG사 구분코드**

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 **`daou`** 로 지정하셔야 합니다.



**`pay_method`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**결제수단 구분코드**

* card(신용카드)
* trans(실시간 계좌이체)
* vbank(가상계좌)



**`merchant_uid`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**주문번호**

매번 고유하게 채번되어야 합니다.



**`digital`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**디지털 컨텐츠 여부**

가맹점 <> 페이조아간 계약 상태에 따라 정해진 올바른 값을 넣어야 함. 그렇지 않은 경우 결제 진행 불가



**`bypass.daou.PRODUCTCODE`` `**<mark style="color:green;">**`string`**</mark>

**결제 상품 고유 번호**

값에 대해 정해진 규격이 없고 보내지 않을 경우 아임포트가 기본값(iamport)을 설정해 페이조아 측으로 전달



**`bypass.daou.CASHRECEIPTFLAG`` `**<mark style="color:green;">**``**</mark><mark style="color:purple;">**`integer`**</mark>

**현금영수증 발급 구분코드 **<mark style="color:green;">****</mark>&#x20;

비 신용결제(계좌,가상)시 페이조아에서 자동발급 여부 구분코드

&#x20;**`1: 허용`**&#x20;

&#x20;**`2: 차단`**&#x20;

&#x20;<mark style="color:green;">****</mark>&#x20;

**`app_scheme`` `**<mark style="color:green;">**`string`**</mark>

**모바일 앱 URL Scheme**

모바일 앱 **** 환경에서 결제시 필수 파라미터&#x20;

****

**`amount`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**결제금액**

<mark style="color:green;">**string**</mark> 이 아닌점에 유의하세요



**`escrow``  `**<mark style="color:orange;">**`boolean`**</mark>

**에스크로 설정여부**&#x20;

계좌이체,가상계좌만 지원됩니다.
{% endtab %}

{% tab title="비 인증 API 요청" %}
#### **API 방식으로 빌링키 발급,결제요청,예약결제를 구현할수 있습니다.**

****

### 일회성 결제 요청하기

REST[ **API POST /subscribe/payments/onetime**](../../api/api-4/api-1.md)을 호출하여 일회성 결제를 요청합니다. 요청 시 전달된 카드는 아임포트에 등록되지 않습니다.

```
curl -H "Content-Type: application/json" \   
     -X POST -d '{"merchant_uid":"order_id_8237352", "card_number":"1234-1234-1234-1234", "expiry":"2019-01", "birth":"123456", "amount":3000}' \
     https://api.iamport.kr/subscribe/payments/onetime
```

###

### 빌링키 발급 요청하기

REST [**API POST /subscribe/customers/{customer\_uid}**](../../api/api-2/api-1.md)를 호출하여 빌링키 발급을 요청합니다.

```
curl -H "Content-Type: application/json" \   
     -X POST -d '{"card_number":"1234-1234-1234-1234", "expiry":"2025-12", "birth":"820213", "pwd_2digit":"00"}' \
     https://api.iamport.kr/subscribe/customers/your-customer-unique-id
```



### 빌링키 발급 및 최초 결제 요청하기

REST [**API POST /subscribe/payments/onetime**](../../api/api-4/api-1.md)을 호출하여 빌링키 발급과 최초 결제를 요청합니다.

* **`customer_uid`** : 빌링키 등록을 위해서 지정해야 합니다.

```
curl -H "Content-Type: application/json" \   
     -X POST -d '{"customer_uid":"your-customer-unique-id", "merchant_uid":"order_id_8237352", "card_number":"1234-1234-1234-1234", "expiry":"2019-01", "birth":"123456", "amount":3000}' \
     https://api.iamport.kr/subscribe/payments/onetime 
```



### 빌링키로 결제 요청하기

빌링키 발급과 최초 결제가 성공하면 빌링키는 전달된 `customer_uid` 와 1:1 매칭되어 아임포트에 저장됩니다. 보안상의 이유로 서버는 빌링키에 직접 접근할 수 없기 때문에 `customer_uid`를 이용해서 재결제([**POST /subscribe/payments/again**](../../api/api-4/api.md)) REST API를 다음과 같이 호출합니다.

```
curl -H "Content-Type: application/json" \   
     -X POST -d '{"customer_uid":"your-customer-unique-id", "merchant_uid":"order_id_8237352", "amount":3000}' \
     https://api.iamport.kr/subscribe/payments/again
```

****

**자세한 가이드는 아래 링크를 참조하세요**

{% content-ref url="../../auth/guide-1/" %}
[guide-1](../../auth/guide-1/)
{% endcontent-ref %}
{% endtab %}
{% endtabs %}

### 3. 부가기능

{% tabs %}
{% tab title="할부개월수 설정" %}
{% code title="javascript" %}
```javascript
display: {
    card_quota: [6]  // 할부개월 6개월까지만 활성화
}
```
{% endcode %}



**파라미터 설명**

* **card\_quota :**
  * `[]`: 일시불만 결제 가능
  * `2,3,4,5,6`: 일시불을 포함한 2, 3, 4, 5, 6개월까지 할부개월 선택 가능\


{% hint style="info" %}
할부결제는 **5만원 이상 결제 요청시**에만 이용 가능합니다.
{% endhint %}
{% endtab %}

{% tab title="에스크로 결제" %}
에스크로 결제를 위해서는 **`escrow`** 파라미터를 추가하고 <mark style="color:red;">**true**</mark> 값으로 설정되어야 합니다.  에스크로 결제가 완료되면 가맹점은 배송정보 등록을 진행해야 하며 해당 작업이 누락되는경우 **정산이 진행되지 않습니다**. [**배송정보 등록**](../../api/api-7/api-1.md) 및 [**배송수정 API**](../../api/api-7/api-2.md) 를 이용하여 배송정보를 관리할 수 있습니다.

{% code title="API Body 예시" %}
```javascript
{
    "logis": {
        "invoice": "1728384716123",
        "company": "CJGLS",
        "receiving_at": "20220215",
        "address": "성수이로20길16"
    },
    "receiver": {
        "name": "홍길동"
    },
    "sender": {
        "relationship": "본인"
    }
}
```
{% endcode %}

{% hint style="danger" %}
**주의사항**

* 에스크로 배송정보 등록/수정시 가맹점이 전달한 배송정보(운송장번호, 택배사이름 등)에 대해 페이조아 측에서 유효성 체크를 하지 않습니다.
{% endhint %}
{% endtab %}
{% endtabs %}

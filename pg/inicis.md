---
description: KG이니시스 결제창 연동 가이드입니다.
---

# ⌨ KG 이니시스

### 1. KG이니시스 PG 설정하기

[**KG이니시스 설정**](../undefined/2.-pg/pg/kg.md) 페이지의 내용을 참고하여 PG 설정을 진행합니다.

![](../.gitbook/assets/7043\_14679\_1310.jpeg)

### 2.결제 요청하기

[JavaScript SDK](../sdk/javascript-sdk/) IMP.**request\_pay**(param, callback)을 호출하여 KG이니시스 결제창을 호출할 수 있습니다. **결제결과**는 PC의 경우 IMP.request\_pay(param, callback) 호출 후 <mark style="color:red;">**callback**</mark>** ** 으로 수신 되며 모바일의 경우<mark style="color:red;">**m\_redirect\_url**</mark>** ** 로 리디렉션됩니다.

{% tabs %}
{% tab title="인증결제창 요청" %}
{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
    pg : 'html5_inicis',
    pay_method : 'card',
    merchant_uid: "order_no_0001", //상점에서 생성한 고유 주문번호
    name : '주문명:결제테스트',
    amount : 1004,
    buyer_email : 'iamport@siot.do',
    buyer_name : '구매자이름',
    buyer_tel : '010-1234-5678',   //필수 파라미터 입니다.
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

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 **`html5_inicis`** 로 지정하셔야 합니다.



**`pay_method`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**결제수단 구분코드**

* `card` (신용카드)
* `samsung` (삼성페이)
* `kakaopay` (카카오페이)
* `ssgpay` (SSG 페이)
* `chai` (차이페이)
* `trans` (실시간 계좌이체)
* `vbank`(가상계좌)
* `phone` (휴대폰소액결제)
* `payco` (페이코 허브형)
* `naverpay` (네이버페이)
* `cultureland` (문화상품권)
* `smartculture` (스마트문상)
* `happymoney` (해피머니)



**`merchant_uid`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**주문번호**

매번 고유하게 채번되어야 합니다.



**`amount`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**결제금액**

<mark style="color:green;">**string**</mark> 이 아닌점에 유의하세요



**`buyer_tel`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**`주문자연락처`**

<mark style="color:red;">필수</mark> 파라미터 입니다.

{% embed url="https://codepen.io/chaiport/pen/rNJpGWO" %}
KG이니시스 결제창 예제
{% endembed %}
{% endtab %}

{% tab title="비인증 결제창 요청" %}
### PG사 결제창으로 카드정보를 입력받고 빌링키를 발급할수 있습니다.

* 인증결제창 호출 파라미터에서 **customer\_uid** 값을 추가하면 비 인증 결제창을 호출할 수 있습니다.&#x20;
* 비 인증 결제창에서 빌링키를 발급받은 후 해당 빌링키로 결제를 요청합니다.
* amount 파라미터에 금액을 설정하여도 실제 승인은 이루어지지 않습니다.



{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
    pg : 'html5_inicis',  // 실제 계약 후에는 실제 상점아이디로 변경
    pay_method : 'card', // 'card'만 지원됩니다.
    merchant_uid: "order_monthly_0001", // 상점에서 관리하는 주문 번호
    name : '최초인증결제',
    amount : 0, // 결제창에 표시될 금액. 실제 승인이 이뤄지지는 않습니다.
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



### 주요 파라미터 설명

**`pg`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**PG사 구분코드**

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 등록된 PG사가 여러개인 경우에는 **`html5_inicis`**로 설정합니다.&#x20;

> KG이니시스에서 발급받은 상점아이디가 여러개(각각 일반 및 정기)인 경우에는 html5\_inicis.{상점아이디} 또는 inicis.{상점아이디}(for ActiveX)로 지정합니다.



**`customer_uid`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**카드 빌링키**

비 인증 결제창에서 고객이 입력한 카드정보와 1:1로 매칭될 빌링키를 지정합니다.



**`amount`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**Integer**</mark>

**결제금액**

결제창에 표시될 금액으로 <mark style="color:red;">실제 승인은 이루어지지 않습니다.</mark>(실 결제를 발생시키기 위해서는 **customer\_uid** 로 **REST API 를 이용하여 결제요청**을 해주셔야 합니다.)\


### 빌링키(customer\_uid)로 결제 요청하기

빌링키 발급이 성공하면 실 빌링키는 customer\_uid 와 1:1 매칭되어 **아임포트 서버에 저장**됩니다. customer\_uid를 가맹점 내부서버에 저장하시고 [<mark style="color:blue;">**비 인증 결제요청 REST API**</mark>](../api/api-4/api.md)를 호출하시면 결제를 발생시킬 수 있습니다.



{% code title="sever-side" %}
```
curl -H "Content-Type: application/json" \   
     -X POST -d '{"customer_uid":"your-customer-unique-id", "merchant_uid":"order_id_8237352", "amount":3000}' \
     https://api.iamport.kr/subscribe/payments/again
```
{% endcode %}
{% endtab %}

{% tab title="비인증 API 방식" %}
### **API 방식으로 빌링키 발급,결제요청,예약결제를 구현할수 있습니다.**

****

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
* **`amount`** : 0원 이상 설정시 빌링키 발급과 동시에 실결제가 발생됩니다.

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

### 3. 부가기능

{% tabs %}
{% tab title="할부개월수 설정" %}
{% code title="javascript" %}
```javascript
display: {
    card_quota: [6]  // 할부개월 6개월만 활성화
}
```
{% endcode %}



**파라미터 설명**

* **card\_quota :** 지정한 숫자에 해당하는 할부개월수만 표기
  * `[]`: 일시불만 결제 가능
  * `2,3,4,5,6`: 일시불을 포함한 2, 3, 4, 5, 6 할부개월 선택 가능\


{% hint style="info" %}
할부결제는 **5만원 이상 결제 요청시**에만 이용 가능합니다.
{% endhint %}



{% embed url="https://codepen.io/chaiport/pen/gOvoxpw" %}
{% endtab %}

{% tab title="카드사 모듈 바로 호출" %}
{% code title="javascript" %}
```javascript
card: {
     direct: {
        code: "367",
        quota: 3
    }
}
```
{% endcode %}



**파라미터 설명**

* **code** : 카드사 금융결제원 표준 코드. [<mark style="color:red;">**링크**</mark>](https://chaifinance.notion.site/53589280bbc94fab938d93257d452216?v=eb405baf52134b3f90d438e3bf763630)  참조 (**string**)
* **quota** : 할부 개월 수. 일시불일 시 0 으로 지정. (**integer**)



{% embed url="https://codepen.io/chaiport/pen/Yzewbeg" %}
<mark style="color:red;">**현대카드**</mark> 결제모듈 바로 호출 예제
{% endembed %}
{% endtab %}

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

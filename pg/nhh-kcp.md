---
description: NHN KCP 결제창 연동 가이드입니다.
---

# ⌨ NHH KCP

### 1. NHH KCP PG 설정하기

****[**NHN KCP 설정**](../undefined/2.-pg/payment-gateway/nhn-kcp.md) 페이지의 내용을 참고하여 PG 설정을 진행합니다.

![](<../.gitbook/assets/스크린샷 2022-05-29 오후 7.53.40.png>)

### 2.결제 요청하기

[JavaScript SDK](../sdk/javascript-sdk/) IMP.**request\_pay**(param, callback)을 호출하여 NHN KCP 결제창을 호출할 수 있습니다. **결제결과**는 PC의 경우 IMP.request\_pay(param, callback) 호출 후 <mark style="color:red;">**callback**</mark>** ** 으로 수신되고 모바일의 경우 <mark style="color:red;">**m\_redirect\_url**</mark>** ** 로 리디렉션됩니다.

{% tabs %}
{% tab title="인증결제창 요청" %}
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

####

### 주요 파라미터 설명

**`pg`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**PG사 구분코드**

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 `kcp`로 지정하셔야 합니다.



**`pay_method`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**결제수단 구분코드**

* card (신용카드)
* samsung (삼성페이)
* trans (실시간 계좌이체)
* vbank(가상계좌)
* phone (휴대폰소액결제)
* payco (페이코 허브형)
* naverpay (네이버페이)
* cultureland (문화상품권)
* smartculture (스마트문상)
* happymoney (해피머니)
* booknlife (도서문화상품권)
* point (베네피아 포인트)
* kakaopay(카카오페이)
* naverpay(네이버페이)



**`merchant_uid`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**주문번호**

매번 고유하게 채번되어야 합니다.



**`amount`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**결제금액**

**string** 이 아닌점에 유의하세요



{% hint style="info" %}
**payco 허브형**인 경우 KCP 관리자페이지 신청 및 설정이 필요합니다.

신청안내 링크 : [https://sir.kr/main/service/p\_payco\_hub.php](https://sir.kr/main/service/p\_payco\_hub.php)
{% endhint %}

{% embed url="https://codepen.io/chaiport/pen/NWXrGvQ" %}
{% endtab %}

{% tab title="비인증 결제창 요청" %}
인증결제창 호출 파라미터에서 **customer\_uid** 값을 추가하면 비 인증 결제창을 호출할 수 있습니다. 비인증 결제창에서 빌링키를 발급받은 후 해당 빌링키로 결제를 요청합니다.

{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
    pg : 'kcp_billing',
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



{% hint style="info" %}
* 비인증 결제를 위해서는 **KCP와 협의가 완료된 사이트코드**를 관리자콘솔에 설정하셔야 비인증 결제창을 활성화 시킬수 있습니다.
* KCP는 빌링키 발급시 <mark style="color:red;">**실 결제는 발생되지 않습니다**</mark>.(금액을 지정해도 결제가 발생되지 않음)
{% endhint %}



### 주요 파라미터 설명

**`pg`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**PG사 구분코드**

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 `kcp_billing`으로 지정합니다.\


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

{% tab title="비인증 API 요청" %}
#### **API 방식으로 빌링키 발급,결제요청,예약결제를 구현할수 있습니다.**

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



### 빌링키 발급 및 최초 결제 요청하기

REST [**API POST /subscribe/payments/onetime**](../api/api-4/api-1.md)을 호출하여 빌링키 발급과 최초 결제를 요청합니다.

* **`customer_uid`** : 빌링키 등록을 위해서 지정해야 합니다.

```
curl -H "Content-Type: application/json" \   
     -X POST -d '{"customer_uid":"your-customer-unique-id", "merchant_uid":"order_id_8237352", "card_number":"1234-1234-1234-1234", "expiry":"2019-01", "birth":"123456", "amount":3000}' \
     https://api.iamport.kr/subscribe/payments/onetime 
```



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



할부개월수 <mark style="color:red;">**3개월**</mark>**까지 활성화 예제**

{% embed url="https://codepen.io/chaiport/pen/yLpMvYJ" %}
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

{% hint style="danger" %}
**주의사항**

* 현재 **KG이니시스, KCP, 토스페이먼츠, 나이스페이먼츠, KICC, 다날** 6개 PG사에 대해서만 카드사 결제창 direct 호출이 가능합니다.
* 일부 PG사의 경우, 모든 상점아이디에 대하여 카드사 결제창 direct 노출 기능을 지원하지 않습니다. 반드시 아임포트를 통해 현재 사용중인 상점아이디가 카드사 결제창 direct 호출이 가능하도록 설정이 되어있는지 PG사에 확인이 필요합니다.
{% endhint %}

<mark style="color:red;">****</mark>\ <mark style="color:red;">**현대카드**</mark> 결제모듈 바로 호출 예제

{% embed url="https://codepen.io/chaiport/pen/oNpZEvq" %}
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

<mark style="color:orange;">****</mark>

<mark style="color:red;">**신한카드**</mark>**만 결제창 노출 처리 예제**

{% embed url="https://codepen.io/chaiport/pen/RwxpQNq" %}
{% endtab %}

{% tab title="앱카드 결제만 노출" %}
인증결제시 각 카드사 앱카드 결제 화면만 노출하고 싶은 경우 아래 파라미터를 설정하시면 됩니다.

{% code title="request_pay()" %}
```javascript
...
appCard : true .  //true 설정시 각 카드사 앱카드 결제만 활성화
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

### 4. 기타 파라미터

{% tabs %}
{% tab title="상품권 결제수단" %}
**상품권 결제수단**을 사용하기 위해서는 가맹점에서 관리하는 회원ID를 아래와 같은 방법으로 파라미터 설정이 필요합니다.

{% code title="javascript SDK " %}
```javascript
bypass : {
    shop_user_id : ‘ABCD123’   //가맹점 회원ID (20byte)
}
```
{% endcode %}

{% hint style="success" %}
**상품권 기관 RM 조치를 위해 필수적으로 실어주셔야 합니다.**&#x20;
{% endhint %}



**컬처랜드 문화 상품권을 호출하는 경우**

```javascript
MP.request_pay({
    pg : 'kcp.{문화상품권 대상 사이트코드}',
    pay_method : 'cultureland',    //문화상품권
    merchant_uid: "A00021-TEST",
    name : '당근 10kg',
    amount : 1004,
    buyer_email : 'iamport@chai.finance',
    buyer_name : '아임포트 기술지원팀',
    buyer_tel : '010-1234-5678',
    buyer_addr : '서울특별시 강남구 삼성동',
    buyer_postcode : '123-456',
    bypass : {
        shop_user_id : 'abaddd'  // 가맹점 회원 id기재
    }
}
```
{% endtab %}

{% tab title="에스크로 결제" %}
에스크로 결제를 위해서는 **`escrow`** 파라미터를 추가하고 **true** 값으로 설정되어야 합니다. 에스크로 결제요청 시 **장바구니 상품을 묶어서 결제하는 경우** 해당 품목에 대한 정보를 전달하기 위해 해당 상품관련 정보를 추가 파라미터(**`kcpProducts`**)로 전달해야 합니다.\
**`kcpProducts`**는 다음 4개의 필수 속성으로 구성된 객체배열입니다.&#x20;



**`amount`** 값은 결제 금액(`param.amount`) 값과 관계가 없으며 비교검증되지 않습니다.

* orderNumber : 상품주문번호
* name : 상품명
* quantity : 수량
* amount : 상품 가격



{% code title="JavaScript SDK" %}
```javascript
IMP.request_pay({
    pg : 'kcp',
    escrow : true, //에스크로 결제인 경우 필요
    kcpProducts : [
    	{
	    "orderNumber" : "xxxx",
	    "name" : "상품A",
	    "quantity" : 3,
	    "amount" : 1000
	},{
	    "orderNumber" : "yyyy",
	    "name" : "상품B",
	    "quantity" : 2,
	    "amount" : 3000
	}
    ],
    //* ...중략 (README 파일에서 상세 샘플코드를 확인하세요)... *//
})
```
{% endcode %}
{% endtab %}
{% endtabs %}

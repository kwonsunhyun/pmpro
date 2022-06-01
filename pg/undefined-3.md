---
description: 다날 결제연동 방법을 안내합니다.
---

# ⌨ 다날

### 1. 다날 PG 설정하기

****[**다날 일반결제 테스트 모드 설정**](../undefined/2.-pg/pg/undefined-5.md) **** 페이지의 내용을 참고하여 PG 설정을 진행합니다.

![](<../.gitbook/assets/스크린샷 2022-05-30 오후 5.30.00.png>)

### 2.결제창 요청하기

[JavaScript SDK](../sdk/javascript-sdk/) IMP.**request\_pay**(param, callback)을 호출하여 다날 Tpay 결제창을 호출할 수 있습니다. **결제결과**는 PC의 경우 IMP.request\_pay(param, callback) 호출 후 **callback**으로 수신되 모바일의 경우 **m\_redirect\_url**로 리디렉션됩니다.



{% tabs %}
{% tab title="인증결제창 요청" %}
{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
    pg : 'danal_tpay',
    pay_method : 'card',
    merchant_uid: "order_no_0001", //상점에서 생성한 고유 주문번호
    name : '주문명:결제테스트',
    amount : 1004,
    buyer_email : 'iamport@siot.do',
    buyer_name : '구매자이름',
    buyer_tel : '010-1234-5678',
    buyer_addr : '서울특별시 강남구 삼성동',
    buyer_postcode : '123-456'
}, function(rsp) { // callback 로직
	//* ...중략... *//
});
```
{% endcode %}

####

### 주요 파라미터 설명

**`pg`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**PG사 구분코드**

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 **`danal_tpay`** 로 지정하셔야 합니다.



**`pay_method`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**결제수단 구분코드**

* card (신용카드)
* trans (실시간 계좌이체)
* vbank(가상계좌)
* cultureland (문화상품권)
* happymoney (해피머니)
* booknlife (도서문화상품권)



**`merchant_uid`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**`주문번호`**

매번 고유하게 채번되어야 합니다.



**`buyer_tel`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**`주문자 연락처` **<mark style="color:green;">****</mark>&#x20;

미 설정 시 다날 결제창에서 오류 발생 가능



**`amount`**<mark style="color:red;">**`*`**</mark><mark style="color:purple;">**`integer`**</mark>

**결제금액**

<mark style="color:green;">**string**</mark> 이 아닌점에 유의하세요



{% hint style="info" %}
#### 가상계좌 결제창 호출시 주의사항

* **`biz_num`**: `사업자등록번호 10자리` 필수 입력 (미설정 시 다날 결제창에서 오류 발생 가능)
{% endhint %}



{% embed url="https://codepen.io/chaiport/pen/jOZZgGG" %}
{% endtab %}

{% tab title="비인증 결제창 요청" %}
인증결제창 호출 파라미터에서 **customer\_uid** 값을 추가하면 비 인증 결제창을 호출할 수 있습니다.   &#x20;



{% hint style="danger" %}
#### **amount 금액**

* 빌링키 발급시 amount 파라미터에 금액이 설정되는 경우 **실 결제와 동시에 빌링키가 발급**됩니다.
* 실결제를 원하지 않은 경우 amount 금액을 <mark style="color:red;">**0원**</mark>으로 설정합니다.

(amount를 0으로 지정한 경우 다날에서 최초 10원 테스트 결제를 하고 30분 쯤 후 자동 취소됩니다.)
{% endhint %}



{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
   pg : 'danal_tpay',
   pay_method : 'card', // 'card'만 지원됩니다.
   merchant_uid: "order_monthly_0001", // 상점에서 관리하는 주문 번호
   name : '최초인증결제',
   amount : 0, // 빌링키 발급만 진행하며 결제승인을 하지 않습니다.
   customer_uid : 'your-customer-unique-id', // 필수 입력.
   buyer_email : 'iamport@siot.do',
   buyer_name : '아임포트',
   buyer_tel : '02-1234-1234',    
   buyer_addr : '서울특별시 강남구 삼성동'
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

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 **`danal_tpay`** 으로 지정합니다.\


**`customer_uid`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**카드 빌링키**

비 인증 결제창에서 고객이 입력한 카드정보와 1:1로 매칭될 빌링키를 지정합니다.



**`amount`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**Integer**</mark>

**결제금액**

0원으로 설정시 빌링키만 발급되며 **0원 이상 설정시 실결제와 빌링키 발급이 동시**에 이루어 집니다.\


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
  * `3,6`: 일시불을 포함한 3, 6개월 할부개월 선택 가능\


{% hint style="info" %}
할부결제는 **5만원 이상 결제 요청시**에만 이용 가능합니다.
{% endhint %}



할부개월수 <mark style="color:red;">**3개월**</mark>**까지 활성화 예제**

{% embed url="https://codepen.io/chaiport/pen/mdXXNXV" %}
{% endtab %}

{% tab title="카드사 모듈 바로 호출" %}
{% code title="javascript" %}
```javascript
card: {
     direct: {
        code: "367",
        quota: 3,
        usePoint : “Y”
    }
}
```
{% endcode %}



**파라미터 설명**

* **code** : 카드사 금융결제원 표준 코드. [<mark style="color:red;">**링크**</mark>](https://chaifinance.notion.site/53589280bbc94fab938d93257d452216?v=eb405baf52134b3f90d438e3bf763630)  참조 (**string**)
* **quota** : 할부 개월 수. 일시불일 시 0 으로 지정. (**integer**)
* **usePoint** : 해당 파라미터 설정시 카드사 포인트가 후취방식으로 결제됩니다.

{% hint style="danger" %}
**주의사항**

* 카드사 모듈 바로 호출을 이용하기 위해서는 다날측 설정이 우선 필요 합니다.
{% endhint %}
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

{% embed url="https://codepen.io/chaiport/pen/WNMMVJZ" %}
{% endtab %}
{% endtabs %}

---
description: KG모빌리언스 결제 연동 방법을 안내합니다.
---

# ⌨ KG모빌리언스

### 1. KG모빌리언스 PG 설정하기

****[**KG모빌리언스 설정**](../../undefined/2.-pg/pg/kg-1.md) 페이지의 내용을 참고하여 PG 설정을 진행합니다.

![](<../../.gitbook/assets/스크린샷 2022-06-03 오후 7.34.26.png>)

### 2.결제 요청하기

[JavaScript SDK](../../sdk/javascript-sdk/) IMP.**request\_pay**(param, callback)을 호출하여 KG 모빌리언스 결제창을 호출할 수 있습니다. **결제결과**는 PC의 경우 IMP.request\_pay(param, callback) 호출 후 <mark style="color:red;">**callback**</mark>** ** 으로 수신되고 모바일의 경우<mark style="color:red;">**m\_redirect\_url**</mark>** ** 로 리디렉션됩니다.

{% tabs %}
{% tab title="인증결제창 요청" %}
{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
    pg : 'mobilians',
    pay_method : 'phone',
    merchant_uid: "order_no_0001", //상점에서 생성한 고유 주문번호
    name : '주문명:결제테스트',
    amount : 1004,
    buyer_email : 'iamport@siot.do',
    buyer_name : '구매자이름',
    buyer_tel : '010-1234-5678',  //필수 
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

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 **`mobilians`** 로 지정하셔야 합니다.



**`pay_method`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**결제수단 구분코드**

* phone(휴대폰소액결제)



**`merchant_uid`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**주문번호**

매번 고유하게 채번되어야 합니다.



**`amount`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**결제금액**

<mark style="color:green;">**string**</mark> 이 아닌점에 유의하세요



{% embed url="https://codepen.io/chaiport/pen/zYRapvw" %}
{% endtab %}

{% tab title="결제창 방식 비 인증 결제" %}
인증결제창 호출 파라미터에서 **customer\_uid** 값을 추가하면 비 인증 결제창을 호출할 수 있습니다. 비 인증 결제창에서 빌링키를 발급받은 후 해당 빌링키로 결제를 요청합니다.

{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
    pg : 'mobilians',
    pay_method : 'phone',
    merchant_uid: "order_monthly_0001", // 상점에서 관리하는 주문 번호
    name : '최초인증결제',
    amount : 1004, // 결제창에 표시될 금액. 실제 승인이 이뤄지지는 않습니다.
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
* 비 인증 결제를 위해서는 **KG모빌리언스와 계약이 완료된 MID 정보를** 관리자콘솔에 설정하셔야 비 인증 결제창을 활성화 시킬수 있습니다.
* **KG모빌리언스 휴대폰 결제는** 빌링키 발급시 <mark style="color:red;">**실 결제가 발생됩니다.**</mark>
* 최초 승인일자 기준 매월 ** **<mark style="color:red;">**동일한 일자에 동일금액**</mark>이 재 결제되어야 합니다.
{% endhint %}



### 주요 파라미터 설명

**`pg`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**PG사 구분코드**

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 ``mobilians`.MID`로 지정합니다.\


**`customer_uid`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**카드 빌링키**

비 인증 결제창에서 고객이 입력한 카드정보와 1:1로 매칭될 빌링키를 지정합니다.



**`amount`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**Integer**</mark>

**결제금액**

결제창에 표시될 금액으로 <mark style="color:red;">실제 승인이 발생됩니다.</mark>

(실 결제를 발생시키기 위해서는 **customer\_uid** 로 **REST API 를 이용하여 결제요청**을 해주셔야 합니다.)\


### 빌링키(customer\_uid)로 결제 요청하기

빌링키 발급이 성공하면 실 빌링키는 customer\_uid 와 1:1 매칭되어 **아임포트 서버에 저장**됩니다. customer\_uid를 가맹점 내부서버에 저장하시고 [<mark style="color:blue;">**비 인증 결제요청 REST API**</mark>](../../api/api-4/api.md) <mark style="color:red;"></mark> 를 호출하시면 결제를 발생시킬 수 있습니다.

{% code title="sever-side" %}
```
curl -H "Content-Type: application/json" \   
     -X POST -d '{"customer_uid":"your-customer-unique-id", "merchant_uid":"order_id_8237352", "amount":1004}' \
     https://api.iamport.kr/subscribe/payments/again
```
{% endcode %}
{% endtab %}

{% tab title="비 인증 API 요청" %}
**아임포트를 통한 KG 모빌리언스는 API 방식 비 인증 결제는 지원되지 않습니다.**
{% endtab %}
{% endtabs %}

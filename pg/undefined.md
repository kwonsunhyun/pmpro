---
description: 페이먼트월 결제창 연동가이드를 확인 합니다.
---

# ⌨ 페이먼트월

### 1. 페이먼트월 PG 설정하기

[**페이먼트월 일반결제 테스트 모드 설정**](../undefined/2.-pg/pg/undefined-1-1.md) 페이지의 내용을 참고하여 PG 설정을 진행합니다.

![](../.gitbook/assets/Paymentwall\_logo\_dark\_latest.jpeg)

### 2.결제창 요청하기

[JavaScript SDK](../sdk/javascript-sdk/) IMP.**request\_pay**(param, callback)을 호출하여 페이먼트월 결제창을 호출할 수 있습니다. **결제결과**는 PC의 경우 IMP.request\_pay(param, callback) 호출 후 **callback**으로 실행되고 모바일의 경우**m\_redirect\_url** 로 리디렉션됩니다.

{% tabs %}
{% tab title="인증결제창 요청" %}
{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
    pg : 'paymentwall',
    pay_method : 'card', // 페이먼트월은 국가IP에 따라 결제수단이 활성화 됩니다.(생략가능)
    merchant_uid: "order_no_0001", //상점에서 생성한 고유 주문번호
    name : '주문명:결제테스트',
    amount : 1004,
    currency : 'KRW'  // 필수 파라미터
    buyer_email : 'iamport@siot.do',  //필수 파라미터 
    buyer_name : 'Jack Son',   //반드시 Firstname Lastname 이 빈칸으로 구분되어야 
    buyer_tel : '010-1234-5678',
    buyer_addr : '서울특별시 강남구 삼성동',
    buyer_postcode : '123-456',
    m_redirect_url : '{모바일에서 결제 완료 후 리디렉션 될 URL}',
    bypass: {
      //터미날3 인경우 해당 파라미터 설정, 미 설정시 Defualt(일반) 결제창 활성화
      widget_code: "t3_1",  
      // 특정 결제수단만 활성화 하는 경우 사용 all 인 경우(default) 국가 지원 결제수단 모두 표
      ps : "all"  
    },
    
}, function(rsp) { // callback 로직
	//* ...중략... *//
});
```
{% endcode %}

####

### 주요 파라미터 설명

**`pg`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**PG사 구분코드**

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 **`paymentwall`** 로 지정하셔야 합니다.



**`pay_method`** <mark style="color:red;">****</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**결제수단 구분코드 (생략가능)**

결제수단 제어는 [페이먼트월 홈페이지](https://api.paymentwall.com/) 안에서 Project를 활성화 하여 제어 할수 있습니다.&#x20;

(별도로 제어하지 않으시면 국가IP에 맞는 결제수단이 기본으로 노출됩니다)



**`merchant_uid`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**주문번호**

매번 고유하게 채번되어야 합니다.



**`amount`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**결제금액**

<mark style="color:green;">**string**</mark> 이 아닌점에 유의하세요



**`buyer_name`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**`구매자 이름`**

**First name** 과 **Last name** 이 <mark style="color:red;">**빈칸**</mark>으로 구분되어 반드시 유입되어야 합니다.



**`buyer_email`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**`구매자 email 주소` **<mark style="color:green;">****</mark>&#x20;

필수로 유입되어야 합니다.



**`currency`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**`통화구분코드` **<mark style="color:green;">****</mark>&#x20;



**`bypass`**

**`페이먼트월 전용 파라미터` **&#x20;

* **`widget_code` :**  터미날3 인 경우 <mark style="color:red;">**t3\_1**</mark>  파라미터 설정, 미 설정시 Defualt(일반) 결제창 활성화
* **`ps` :**  특정 결제수단만 활성화 하는 경우 사용합니다. 해당 파라미터에 설정할 코드표는 [**링크**](https://docs.paymentwall.com/reference/payment-system-shortcodes)를 참조해 주세요.   ex) `kakaopaykr` = 카카오페이
{% endtab %}

{% tab title="비 인증 결제" %}
서비스 준비
{% endtab %}
{% endtabs %}

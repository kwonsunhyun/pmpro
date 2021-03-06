---
description: 엑심베이 결제 연동 방법을 안내합니다.
---

# ⌨ 엑심베이

### 1. 엑심베이 PG 설정하기

****[**엑심베이 설정**](../../ready/2.-pg/payment-gateway/undefined-7.md) **** 페이지의 내용을 참고하여 PG 설정을 진행합니다.

![](<../../.gitbook/assets/스크린샷 2022-06-03 오후 3.34.40.png>)

### 2.결제 요청하기

[JavaScript SDK](../../sdk/javascript-sdk/) IMP.**request\_pay**(param, callback)을 호출하여 엑심베이 결제창을 호출할 수 있습니다. **결제결과**는 **PC / 모바일** 모두 <mark style="color:red;">**callback**</mark> 으로 전달됩니다.&#x20;

{% tabs %}
{% tab title="인증결제창 요청" %}
{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
    pg : 'eximbay',
    pay_method : 'card',
    merchant_uid: "order_no_0001", // 상점에서 관리하는 주문 번호
    name : '주문명:결제테스트',
    amount : 14.20,
    currency : 'USD', // 기본값: USD(원화 KRW는 페이팔 정책으로 인해 지원하지 않음)
    buyer_email : 'iamport@siot.do',
    buyer_name : '구매자이름',
    buyer_tel : '010-1234-5678',
    buyer_addr : '서울특별시 강남구 삼성동',
    buyer_postcode : '123-456',
}, function(rsp) { // callback 로직
	//* ...중략... *//
});
```
{% endcode %}

####

### 주요 파라미터 설명

**`pg`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**PG사 구분코드**

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 **`eximbay`** 로 지정하셔야 합니다.



**`pay_method`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**결제수단 구분코드**

* 신용카드: card
* 위챗 : wechat  &#x20;
* 알리페이 : alipay  &#x20;
* 해외카드 : card  &#x20;
* 유니온페이 : unionpay  &#x20;
* 텐페이 : tenpay
* 일본 편의점결제(eContext) :  econtext



**`merchant_uid`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**`주문번호`**

매번 고유하게 채번되어야 합니다.



**`buyer_tel`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**`주문자 연락처` **<mark style="color:green;">****</mark>&#x20;

&#x20;<mark style="color:green;">****</mark>&#x20;

**`amount`**<mark style="color:red;">**`*`**</mark><mark style="color:purple;">**`integer`**</mark>

**결제금액**

<mark style="color:green;">**string**</mark> 이 아닌점에 유의하세요



**`currency`**<mark style="color:green;">**`string`**</mark>

**결제통화코드 **<mark style="color:green;">****</mark>&#x20;

* KRW    &#x20;
* USD    &#x20;
* EUR    &#x20;
* GBP     &#x20;
* JPY    &#x20;
* THB    &#x20;
* SGD    &#x20;
* RUB    &#x20;
* HKD    &#x20;
* CAD    &#x20;
* AUD



**`language`` `**<mark style="color:green;">**`string`**</mark>

* 한국어 : ko  &#x20;
* 영어 : en  &#x20;
* 중국어 : zh   &#x20;
* 일본어 : jp
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
### 참고사항

아임포트는 엑심베이 정기결제를 지원하지 않습니다.
{% endhint %}

<details>

<summary>편의점 결제 테스트 방법</summary>

### **편의점결제 동작 방식**

한국의 가상계좌와 같이 결제창 내에서는 등록을 한 다음에 고객에게 이메일 / 문자로 전달되는 화면을 편의점 카운터에서 지불하며 처리합니다.

* 아임포트 내부에서는 pay\_method : vbank 로 기록됨
* Econtext 등록이 완료되었다는 콜백함수 및 웹훅 전송 (status : ready 상태 / vbank\_num 은 unknown 으로 고정)
* Econtext 로부터 입금확인이 되면 아임포트에서 엑심베이로부터 응답을 받아 status : paid 로 변경 후 결제완료처리에 대한 웹훅 전송

### **편의점결제 테스트 진행순서**

가상계좌와 같이 실제 고객이 입금한 결과를 테스트해야 하므로 아래와 같이 입금완료됨을 임의적으로 통지받아보실 수 있습니다**.**

1.엑심베이 테스트모드 ON상태에서 1번과 같이 결제창 진행

2\. 콜백 응답 중 pg\_tid 값을 별도로 메모 (아임포트 관리자콘솔 **** PG사승인번호 컬럼에서 확인 가능) ****&#x20;

3\. [http://test.econ.ne.jp/site/tuchi\_2/tuchi\_menu\_2.html](http://test.econ.ne.jp/site/tuchi\_2/tuchi\_menu\_2.html) 로 이동 후 계정 로그인 &#x20;

&#x20;  (아이디 : ectest / 비번 : #eg0810# ) ****&#x20;

4\. ShopID : 361301, orderID : 2번에서 확보한 PG사승인번호 입력 ****&#x20;

5\. 하단에 있는 **登録** 버튼 클릭 ****&#x20;

6\. 다음 페이지에서 한 번 더 **登録** 클릭 ****&#x20;

7\. 10분 후 결제상태가 status : **paid** 로 바뀌는지 확인 ( 이 때 입금에 대한 웹훅 발송됨 )

</details>

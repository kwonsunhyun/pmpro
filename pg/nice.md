---
description: 나이스페이먼츠 결제창 연동 가이드를 안내합니다.
cover: ../.gitbook/assets/스크린샷 2022-05-29 오후 7.44.33.png
coverY: 0
---

# ⌨ NICE페이먼츠

### 1. PG 설정하기

[**나이스페이먼츠 일반결제 테스트 모드 설정**](../undefined/2.-pg/pg/undefined.md) 페이지의 내용을 참고하여 PG 설정을 진행합니다.

### 2.결제창 요청하기

[JavaScript SDK](../sdk/javascript-sdk/) IMP.**request\_pay**(param, callback)을 호출하여 NICE페이먼츠 결제창을 호출할 수 있습니다. **결제결과**는 PC의 경우 IMP.request\_pay(param, callback) 호출 후 **callback**으로 실행되고 모바일의 경우**m\_redirect\_url**로 리디렉션됩니다.

{% tabs %}
{% tab title="인증결제창 요청" %}
{% code title="Javascript SDK" %}
```javascript
IMP.request_pay({
    pg : 'nice',
    pay_method : 'card',
    merchant_uid: "order_no_0001", //상점에서 생성한 고유 주문번호
    name : '주문명:결제테스트',
    amount : 1004,
    buyer_email : 'iamport@siot.do',
    buyer_name : '구매자이름',
    buyer_tel : '010-1234-5678',
    buyer_addr : '서울특별시 강남구 삼성동',
    buyer_postcode : '123-456',
    m_redirect_url : '{모바일에서 결제 완료 후 리디렉션 될 URL}',
    niceMobileV2 : true  // 신규 모바일 버전 적용 시 설정 
}, function(rsp) { // callback 로직
	//* ...중략... *//
});
```
{% endcode %}

####

### 주요 파라미터 설명

**`pg`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**PG사 구분코드**

관리자페이지에 등록된 PG사가 하나일 경우에는 해당 파라미터 미 설정시 `기본 PG사`가 자동으로 적용되며 여러개인 경우에는 **`nice`** 로 지정하셔야 합니다.



**`pay_method`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**결제수단 구분코드**

* card(신용카드)
* samsung(삼성페이)
* trans(실시간 계좌이체)
* vbank(가상계좌)
* phone(휴대폰소액결제)
* payco(페이코 허브형)
* naverpay(네이버페이)
* kakaopay(카카오페이)



**`merchant_uid`** <mark style="color:red;">**\***</mark>** **<mark style="color:green;">**s**</mark><mark style="color:green;">**tring**</mark>

**주문번호**

매번 고유하게 채번되어야 합니다.



**`amount`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**결제금액**

**string** 이 아닌점에 유의하세요



**`niceMobileV2``  `**<mark style="color:orange;">**`boolean`**</mark>

나이스 모바일 신규버전 적용 여부(기본 값: false)



**`escrow``  `**<mark style="color:orange;">**`boolean`**</mark>

**에스크로 설정여부**&#x20;



{% embed url="https://codepen.io/chaiport/pen/qBxbGXy" %}
나이스페이먼츠 결제창 예제
{% endembed %}
{% endtab %}

{% tab title="비인증 결제창 요청" %}
나이스페이먼츠는 비인증 결제는 차이포트 [**비인증결제 API**](../api/api-4/) 로만 지원 됩니다.

따라서 비인증 결제를 연동하기 위해서는 카드정보를 획득할수 있는 UI를 구성해 주셔야 하며&#x20;

해당 가이드는 [**링크**](../undefined-1/undefined-1/undefined/rest-api.md)에서 확인해주시면 됩니다.

{% hint style="info" %}
**나이스페이먼츠 빌링키 발급은 실 결제 발생이 없이 빌링키만 발급가능 합니다.**
{% endhint %}
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





{% embed url="https://codepen.io/chaiport/pen/poagmae" %}
할부개월수 <mark style="color:red;">**3개월**</mark>**까지 활성화 예제**
{% endembed %}
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

<mark style="color:orange;">****</mark>

{% embed url="https://codepen.io/chaiport/pen/MWQKdVo" %}
<mark style="color:red;">**신한카드**</mark>**만 결제창 노출 처리 예제**
{% endembed %}
{% endtab %}
{% endtabs %}

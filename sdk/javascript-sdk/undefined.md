---
description: 결제요청 파라미터를 확인 할 수 있습니다.
---

# 💿 결제요청 파라미터

## 결제요청 파라미터 정의

> **`pg`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>
>
> **PG사 구분코드**
>
> 해당 코드가 누락되거나 매칭되는 코드가 없는 경우 관리자 콘솔 기본 PG가 호출됩니다.

<details>

<summary>상세코드 확인하기</summary>

* `html5_inicis`(이니시스웹표준)
* `inicis`(이니시스ActiveX결제창)
* `kcp`(NHN KCP)
* `kcp_billing`(NHN KCP 정기결제)
* `uplus`(토스페이먼츠(구 LG U+))
* `nice`(나이스페이)
* `jtnet`(JTNet)
* `kicc`(한국정보통신)
* `bluewalnut`(블루월넛)
* `kakaopay`(카카오페이)
* `danal`(다날휴대폰소액결제)
* `danal_tpay`(다날일반결제)
* `mobilians`(모빌리언스 휴대폰소액결제)
* `chai`(차이 간편결제)
* `syrup`(시럽페이)
* `payco`(페이코)
* `paypal`(페이팔)
* `eximbay`(엑심베이)
* `naverpay`(네이버페이-결제형)
* `naverco`(네이버페이-주문형)
* `smilepay`(스마일페이)
* `alipay`(알리페이)
* `paymentwall`(페이먼트월)
* `eximbay`(엑심베이)
* `tosspay`(토스간편결제)
* `smartro`(스마트로)
* `settle`(세틀뱅크)

</details>

> **`pay_method`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>
>
> **결제수단 구분코드**
>
> PG사별 지원되는 결제수단이 모두 상이합니다.
>
> [**각 PG사별 결제 연동 가이드**](broken-reference)를 참고하세요

<details>

<summary>상세코드 확인하기</summary>

* `card` (신용카드)
* `trans`(실시간계좌이체)
* `vbank`(가상계좌)
* `phone`(휴대폰소액결제)
* `samsung`(삼성페이)
* `kpay`(KPay앱 )
* `kakaopay`(카카오페이)
* `payco`(페이코)
* `lpay`(LPAY)
* `ssgpay`(SSG페이)
* `tosspay`(토스간편결제)
* `cultureland`(문화상품권 )
* `smartculture`(스마트문상)
* `happymoney`(해피머니)
* `booknlife`(도서문화상품권)
* `point`(베네피아 포인트 등 포인트 결제 )
* `wechat`(위쳇페이)
* `alipay`(알리페이)
* `unionpay`(유니온페이)
* `tenpay`(텐페이)

</details>

> **`escrow`    **<mark style="color:orange;background-color:yellow;">**boolean**</mark>** **&#x20;
>
> **에스크로 결제창 활성화 여부**
>
> * [x] 에스크로 설정은 PG사와 협의 이후 진행되어야 하는점 주의하세요

> **`merchant_uid`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>
>
> **가맹점 주문번호**
>
> * 주문번호는 매 결제 요청시 고유하게 채번 되어야 합니다.
> * 40Byte 이내로 작성해주세요
> * 결제 승인완료 처리된 주문번호를 동일하게 재 설정시 사전거절 처리 됩니다.

> **`name`    **<mark style="color:green;">**string**</mark>
>
> **결제대상 제품명**
>
> * 16byte  이내로 작성해주세요

> **`amount`  **<mark style="color:red;">**\***</mark>**   **<mark style="color:purple;">**number**</mark>
>
> **결제금액**
>
> * 숫자타입으로 지정해야 하는점 유의하세요

> **`custom_data`    **<mark style="color:blue;">**object**</mark>
>
> **사용자 정의 데이타**
>
> * 결제 응답시 **echo** 로 받아보실수 있는 필드 입니다.
> * JSON notation(string)으로 저장됩니다.
> * 주문 건에 대해 부가정보를 저장할 공간이 필요할 때 사용합니다

> **`tax_free`    **<mark style="color:purple;">**number**</mark>
>
> **면세금액**
>
> * 결제 금액 중 면세금액에 해당하는 금액을 입력합니다.

> **`currency`    **<mark style="color:green;">**string**</mark>
>
> **결제통화 구분코드**
>
> * PayPal은 원화(KRW) 미 지원으로 USD가 기본
> * PayPal에서 지원하는 통화는 [PayPal 지원 통화](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/%20target=) 참조

<details>

<summary>상세코드 확인하기</summary>

**결제통화 구분코드**

1. KRW
2. USD
3. EUR
4. JPY

* PayPal은 원화(KRW) 미 지원으로 USD가 기본
* PayPal에서 지원하는 통화는 [PayPal 지원 통화](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/%20target=) 참조

</details>

> **`language`    **<mark style="color:green;">**string**</mark>
>
> **결제창 언어 설정** (지원되지 않은 일부 PG사 존재)

<details>

<summary>상세코드 확인하기</summary>

* en (영어)
* ko (한국어)

</details>

> **`buyer_name`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>
>
> **주문자명**

> **`buyer_tel`    **<mark style="color:green;">**string**</mark>
>
> **주문자 연락처**
>
> * 일부 PG사에서 해당 필드 누락시 오류 발생 (엑심베이)

> **`buyer_email`    **<mark style="color:green;">**string**</mark>
>
> **주문자 이메일**
>
> * 일부 PG사에서 해당 필드 누락시 오류 발생(페이먼트월)

> **`buyer_addr`    **<mark style="color:green;">**string**</mark>
>
> **주문자 주소**

> **`buyer_postcode`    **<mark style="color:green;">**string**</mark>
>
> **주문자 우편번호**

> **`confirm_url`    **<mark style="color:green;">**string**</mark>
>
> <mark style="color:green;">****</mark>[**confirm\_process**](../../tip/confirm-process.md) **사용 시 가맹점 endpoint url 설정**
>
> * 기술지원 메일로 별도 요청이 필요합니다. (support@iamport.kr)

> **`notice_url`  **<mark style="color:green;">**string**</mark>
>
> **웹훅(Webhook) 수신 주소**
>
> * 차이포트 관리자 콘솔에 설정한 웹훅 주소대신 사용할 웹훅 주소를 결제시마다 설정할 수 있습니다.
> * 해당 값 설정시 관리자    콘솔에 설정한 주소로는 웹훅발송이 되지 않는점 유의하시기 바랍니다.

> **`customer_uid`**  <mark style="color:green;">**string**</mark>
>
> **가맹점 정의 빌링키**
>
> 비인증 결제 이용시 빌링키와 1:1로 맵핑되는 가맹점 정의 고객 빌링키입니다.

## **추가속성**

> **`digital`    **<mark style="color:orange;">**boolean**</mark>
>
> **디지털 구분자**
>
> * 휴대폰 결제수단인 경우 필수 항목입니다.
> * 결제제품이 실물이 아닌 경우 true 로 설정합니다.
> * 실물/디지털 여부에 따라 수수료율이 상이하게 측정되니 유의하시기 바랍니다.

> **`vbank_due`**  <mark style="color:green;">**string**</mark>&#x20;
>
> **가상계좌 입금기한**
>
> * 결제수단이 가상계좌인 경우 입금기한을 설정할 수 있습니다.
> * YYYYMMDDhhmm 양식으로 구성합니다.

> **`m_redirect_url`    **<mark style="color:green;">**string**</mark>
>
> **결제완료이후 이동될 EndPoint URL 주소**
>
> * 결제창이 새로운 창으로 리다이렉트 되어 결제가 진행되는 결제 방식인 경우 필수 설정 항목 입니다.
> * 대부분의 모바일 결제환경에서 결제창 호출시 필수 항목입니다.
> * 리다이렉트 환경에서 해당 필드 누락시 결제 결과를 수신 받지 못합니다.

> **`app_scheme`**  <mark style="color:green;">**string**</mark>&#x20;
>
> **모바일 앱 결제중 가맹점 앱복귀를 위한 URL scheme**
>
> * WebView 환경 결제시 필수설정 항목 입니다.
> * ISP/앱카드 앱에서 결제정보인증 후 기존 앱으로 복귀할 때 사용합니다.

> **`biz_num`    **<mark style="color:green;">**string**</mark>
>
> **사업자등록번호**
>
> * 다날-가상계좌 결제수단 사용시 필수 항목입니다.

## 부가기능

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
{% endtabs %}


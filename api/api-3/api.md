---
description: 원하는 시점에 결제를 예약하고 결제 결과를 Webhook으로 받을 수 있는 API입니다.
---

# ⌨ 결제 예약 API

### customer\_uid 를 이용하여 비 인증 결제 요청을 예약할수 있는 API 입니다.&#x20;

#### 결제 요청에 대한 결과는 **notice\_url** 에 설정한 EndPoint URL 로 웹훅을 통해 결제 결과를 수신(POST request)받을 수 있습니다.

{% swagger method="post" path="/subscribe/payments/schedule" baseUrl="https://api.iamport.kr" summary="결제 예약(Schedule) API" %}
{% swagger-description %}
customer_uid와 연결된 빌링키로 결제가 예약됩니다. 기존에 발급한 customer_uid 를 이용하지 않고 새로운 값을 지정하는 경우 카드정보를 반드시 기재하여야 하며 요청이 성공적으로 처리되면 빌링키 발급과 결제예약이 동시에 이루어 집니다.
{% endswagger-description %}

{% swagger-parameter in="body" name="customer_uid" type="String" required="true" %}
<mark style="color:red;">

**빌링키**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="checking_amount" type="Integer" %}
유효카드 체크 승인금액
{% endswagger-parameter %}

{% swagger-parameter in="body" name="card_number" type="String" %}
카드번호(

**dddd-dddd-dddd-dddd**

)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiry" type="String" %}
카드 유효기간(

**YYYY-MM**

)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="birth" type="String" %}
생년월일 6자리(**YYMMDD**)

(법인카드의 경우 사업자등록번호10자리)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pwd_2digit" type="String" %}
카드비밀번호 앞 2자리
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cvc" type="String" %}
카드 인증번호 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pg" type="String" %}
pg 구분코드
{% endswagger-parameter %}

{% swagger-parameter in="body" name="schedules" type="array" required="true" %}
<mark style="color:red;">

**결제예약 스케쥴**

</mark>
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="결제예약 성공" %}
{% tabs %}
{% tab title="ScheduleResponse" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**`응답코드`**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**`응답메세지`**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`response`** <mark style="color:red;">**(Array\[ScheduleResultAnnotation], optional)**</mark>
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="ScheduleResultAnnotation" %}
**`code`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**응답메세지**

code값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`customer_uid`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>

**빌링키**

****

**`merchant_uid`  \*  **<mark style="color:green;">**string**</mark>

**주문번호**



**`imp_uid`** <mark style="color:red;">\*</mark> <mark style="color:green;">**string**</mark>

**아임포트 결제 고유 UID**

****

**`schedule_at`    **<mark style="color:red;">**\***</mark>**    **<mark style="color:blue;">**UNIX timestamp**</mark>** **&#x20;

**예약결제 실행 예정 시각**&#x20;

****

**`executed_at`  **<mark style="color:red;">**\***</mark>**    **<mark style="color:blue;">**UNIX timestamp**</mark>

**예약결제가 실행된 시각 **<mark style="color:blue;">****</mark>&#x20;

<mark style="color:blue;">****</mark>

**`revoked_at`  **<mark style="color:red;">**\***</mark>**    **<mark style="color:blue;">**UNIX timestamp**</mark>

**예약결제 실행을 철회한 시각 **<mark style="color:blue;">****</mark>&#x20;

<mark style="color:blue;">****</mark>

**`amount`  **<mark style="color:red;">**\***</mark>**  **<mark style="color:purple;">**integer**</mark>

**주문(결제)금액**

****

**`name`    **<mark style="color:green;">**string**</mark>

**제품명**

****

**`buyer_name`    **<mark style="color:green;">**string**</mark>

**주문자명**

****

**`buyer_email`    **<mark style="color:green;">**string**</mark>

**주문자 Email주소**\
****

**`buyer_tel`    **<mark style="color:green;">**string**</mark>

**주문자 전화번호**

****

**`buyer_addr`    **<mark style="color:green;">**string**</mark>

**주문자 주소**

****

**`buyer_postcode`    **<mark style="color:green;">**string**</mark>

**주문자 우편번호**

****

**`custom_data`    **<mark style="color:green;">**string**</mark>

**echo data JSON string으로 전달**

****

**`schedule_status`  **<mark style="color:blue;">****</mark>**  **<mark style="color:red;">**\***</mark>**  **<mark style="color:blue;">****</mark>** **<mark style="color:green;">**string**</mark>

**예약상태 **<mark style="color:green;">****</mark>&#x20;

* `scheduled`: 예약됨(실행되기 전)
* `executed`: 예약된 결제실행완료
* `revoked`: 예약철회



**`payment_status` **<mark style="color:green;">****</mark>** **<mark style="color:red;">**\***</mark>**  **<mark style="color:blue;">****</mark>** **<mark style="color:green;">**string**</mark>

**실행된 결제의 승인 상태 **<mark style="color:green;">****</mark>&#x20;

* `null`: 아직 예약결제가 실행되지 않음(null 이라는 값의 문자열이 아닌 실제 null 입니다)
* `paid`: 예약결제가 결제승인됨
* `failed`: 예약결제가 승인실패됨
* `cancelled`: 예약결제가 결제승인 후 환불됨



**`fail_reason`    **<mark style="color:green;">**string**</mark>

**실패사유 **<mark style="color:green;">****</mark>&#x20;
{% endtab %}
{% endtabs %}
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="인증 Token이 전달되지 않았거나 유효하지 않은 경우" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

### **주요 요청 파라미터 상세 설명**

> **`schedules`    **<mark style="color:red;">**\***</mark>** **<mark style="color:blue;">**array**</mark>
>
> **결제예약 스케쥴**
>
> ****
>
> <mark style="color:red;">**\[ 필수항목 ]**</mark>
>
> * `merchant_uid` : 가맹점 주문번호(동일한 주문번호로 중복결제 불가)&#x20;
> * `schedule_at` : 결제요청 예약시각 UNIX timestamp
> * `currency` : 외환부호 e.g.) KRW, USD, ...&#x20;
> * `amount` : 결제금액
>
> <mark style="color:green;">**\[ 선택항목 ]**</mark>
>
> * `tax_free` : amount 중 면세공급가액(기본값 : 0)
> * `name` : 주문명(누락되면 아임포트 자체 기본값 사용)
> * `buyer_name` : 주문자명
> * `buyer_email` : 주문자Email
> * `buyer_tel` : 주문자 전화번호
> * `buyer_addr` : 주문자 주소
> * `buyer_postcode` : 주문자 우편번호
> * `custom_data` : 결제수행 시 사용될 custom\_data 값
> * `notice_url` : 예약결제수행 후 통지될 Notification URL&#x20;
>
> &#x20;                               (지정되지 않으면 관리자페이지의 Notification URL로 발송)
>
> * `extra.naverUseCfm` : 이용완료일 YYYYMMDD&#x20;
>
> &#x20;                                              (네이버페이 반복결제 계약 시 이용완료일 필수로 설정된 가맹점에 한함)

{% tabs %}
{% tab title="Schedules Model Schema" %}
{% code title="Sample" %}
```json
[
    {
        "merchant_uid": "your_merchant_uid1",
	"schedule_at": 1478150985,
	"currency": "KRW",
	"amount": 1004,
	"name": "주문명",
	"buyer_name": "주문자명",
	"buyer_email": "주문자 Email주소",
	"buyer_tel": "주문자 전화번호",
	"buyer_addr": "주문자 주소",
	"buyer_postcode": "주문자 우편번호"
},
    {
        "merchant_uid": "your_merchant_uid2",
        "schedule_at": 1478150985,
	"amount": 1004,
	"name": "주문명",
	"buyer_name": "주문자명",
	"buyer_email": "주문자 Email주소",
	"buyer_tel": "주문자 전화번호",
	"buyer_addr": "주문자 주소",
	"buyer_postcode": "주문자 우편번호"
    }
]
```
{% endcode %}
{% endtab %}
{% endtabs %}

> **`pg`    **<mark style="color:red;">**\***</mark>**    **<mark style="color:green;">**string**</mark>
>
> **pg 구분코드**
>
> 관리자콘솔 API 방식 비인증 PG설정이 2개 이상인 경우 필수적으로 기재해야 하는 항목입니다.
>
> 동일 PG사에 <mark style="color:red;">**두개의 MID**</mark> 를 설정한 경우 아래 양식으로 기재 합니다. ****&#x20;
>
> **{PG사}.{PG상점아이디}**
>
> 지정하지 않거나 유효하지 않은 값이 전달되면 기본PG설정된 값을 이용해 결제하게 됩니다.
>
> * 나이스페이먼츠, JTNet 2가지 PG설정이 되어있다면, pg 파라메터로 **nice** 또는 **jtnet**로 구분 가능
> * 나이스페이먼츠로부터 2개 이상의 상점아이디를 발급받았다면, **nice.MID1** 또는 **nice.MID2**로 구분 가능

{% hint style="info" %}
schedules의 상세정보

**buyer\_name, buyer\_email, buyer\_tel, buyer\_addr, buyer\_postcode** 누락시&#x20;

<mark style="color:red;">**customer\_uid**</mark> 에 해당되는 **customer\_name, customer\_email, customer\_tel, customer\_addr, customer\_postcode** 정보로 대체됩니다.
{% endhint %}

<details>

<summary>Request Sample Json</summary>

```
{"customer_uid":"TEST0001","schedules":[{"merchant_uid":"order_id001","schedule_at":1658480415,"amount":1004,"name":"carrot","custom_data":""}]}
```

</details>

<details>

<summary>Response Model Schema</summary>

```json
{
  "code": 0,
  "message": "string",
  "response": [
    {
      "customer_uid": "string",
      "merchant_uid": "string",
      "imp_uid": "string",
      "schedule_at": "0",
      "executed_at": "0",
      "revoked_at": "0",
      "amount": 0,
      "name": "string",
      "buyer_name": "string",
      "buyer_email": "string",
      "buyer_tel": "string",
      "buyer_addr": "string",
      "buyer_postcode": "string",
      "custom_data": "string",
      "schedule_status": "scheduled",
      "payment_status": "paid",
      "fail_reason": "string"
    }
  ]
}
```

</details>

{% hint style="success" %}
**Swagger Test Link**

****[**https://api.iamport.kr/#!/subscribe/schedule**](https://api.iamport.kr/#!/subscribe/schedule)****
{% endhint %}

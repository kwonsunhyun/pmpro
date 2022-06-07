---
description: 아임포트 결제취소 API를 이용한 결제취소 방법을 안내합니다.
---

# 💸 결제취소(환불) 연동하기

### <mark style="color:blue;">**STEP 01.**</mark> 취소 요청하기

필요한 취소 정보를 서버로 전달하여 취소 요청을 진행합니다. 가상계좌 환불의 경우 환불수령 계좌 정보를 추가 파라미터로 전달해야 합니다. 다음은 환불요청을 하기 위해 서버로 해당 정보를 전달하는 예제입니다.

{% tabs %}
{% tab title="HTML" %}
{% code title="client-side" %}
```html
<button onclick="cancelPay()">환불하기</button>
<script
  src="https://code.jquery.com/jquery-3.3.1.min.js"
  integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8="
  crossorigin="anonymous"></script>
<script>
  function cancelPay() {
    jQuery.ajax({
      // 예: http://www.myservice.com/payments/cancel
      "url": "{환불정보를 수신할 가맹점 서비스 URL}", 
      "type": "POST",
      "contentType": "application/json",
      "data": JSON.stringify({
        "merchant_uid": "{결제건의 주문번호}", // 예: ORD20180131-0000011
        "cancel_request_amount": 2000, // 환불금액
        "reason": "테스트 결제 환불" // 환불사유
        // [가상계좌 환불시 필수입력] 환불 수령계좌 예금주
        "refund_holder": "홍길동", 
        // [가상계좌 환불시 필수입력] 환불 수령계좌 은행코드(예: KG이니시스의 경우 신한은행은 88번)
        "refund_bank": "88" 
        // [가상계좌 환불시 필수입력] 환불 수령계좌 번호
        "refund_account": "56211105948400" 
      }),
      "dataType": "json"
    });
  }
</script>
```
{% endcode %}



{% embed url="https://codepen.io/chaiport/pen/jOYXyNd" %}
환불버튼 예제
{% endembed %}
{% endtab %}

{% tab title="React.js" %}
{% code title="client-side" %}
```jsx
class CancelPay extends React.Component {
  cancelPay = () => {
    axios({
      url: "{환불요청을 받을 서비스 URL}", // 예: http://www.myservice.com/payments/cancel
      method: "POST",
      headers: {
        "Content-Type": "application/json,
      },
      data: { 
        merchant_uid: "{결제건의 주문번호}", // 주문번호
        cancel_request_amount: 2000, // 환불금액
        reason: "테스트 결제 환불" // 환불사유
        refund_holder: "홍길동", // [가상계좌 환불시 필수입력] 환불 수령계좌 예금주
        refund_bank: "88" // [가상계좌 환불시 필수입력] 환불 수령계좌 은행코드(예: KG이니시스의 경우 신한은행은 88번)
        refund_account: "56211105948400" // [가상계좌 환불시 필수입력] 환불 수령계좌 번호
      }
    });
  }
  ...
  render() {
    return <button onClick={this.cancelPay}>환불하기</button>;
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### <mark style="color:blue;">**STEP 02.**</mark> 결제정보 조회하기

아래와 같이 결제정보를 저장하는 **`Payments`**라는 테이블을 생성했다고 가정합니다.

{% code title="server-side" %}
```javascript
/* ... model/payments.js ... */
  var mongoose = require('mongoose');
  var Schema = mongoose.Schema;
  ...
  var PaymentsSchema = new Schema({
    imp_uid: String, // 아임포트 `unique key`(환불 요청시 `unique key`로 사용)
    merchant_uid: String, // 주문번호(결제정보 조회시 사용)
    amount: { type: Number, default: 0 }, // 결제 금액(환불 가능 금액 계산시 사용)
    // 환불 된 총 금액(환불 가능 금액 계산시 사용)
    cancel_amount: { type: Number, default: 0 }, 
    ...
  });
  ...
  module.exports = mongoose.model('Payments', PaymentsSchema);
```
{% endcode %}

클라이언트에서 받은 주문번호(**`merchant_uid`**)를 사용해서 해당 주문의 결제정보를 **`Payments`** 테이블에서 조회합니다.

{% code title="server-side" %}
```javascript
/* ... 중략 ... */
  var Payments = require('./models/payments');
  app.post('/payments/cancel', async (req, res, next) => {
    try {
      /* 액세스 토큰(access token) 발급 */
      /* ... 중략 ... */
      /* 결제정보 조회 */
      const { body } = req;
      const { merchant_uid } = body; // 클라이언트로부터 전달받은 주문번호
      Payments.find({ merchant_uid }, async function(err, payment) { 
        if (err) {
          return res.json(err);
        }
        const paymentData = payment[0]; // 조회된 결제정보
        /* 아임포트 REST API로 결제환불 요청 */
        ...
      });
    } catch (error) {
      res.status(400).send(error);
    }
  });

```
{% endcode %}

### <mark style="color:blue;">**STEP 03.**</mark> **차이포트 서버에 취소 요청하기**

취소 요청을 하기 위해서 먼저 [<mark style="color:blue;">**REST API access token**</mark>](../api/rest-api-access-token.md) **** 을 발급받습니다. 발급받은 액세스 토큰(**`access token`**)을 이용하여 [<mark style="color:blue;">**차이포트 취소 API**</mark>](../api/api-1/api.md) <mark style="color:blue;">****</mark> 를 호출하여 결제 취소를 요청합니다.

{% hint style="info" %}
**휴대폰 소액결제 환불 시 유의사항**

* **결제가 이루어진 월과 환불을 요청하는 월이 다를 경우, 전액환불도 불가능**합니다. 예를 들어, 1월 31일 결제건은 2월 1일에 환불할 수 없습니다.
{% endhint %}

#### 아래는 환불요청 시 유의해야 하는 파라미터들입니다.

> **환불 `unique key`**
>
> 환불 대상 거래를 특정하기 위해서 `imp_uid` 또는 `merchant_uid`를 환불 `unique key`로 설정합니다. `imp_uid`의 값이 우선순위를 갖게되며 유효하지 않는 `imp_uid`값을 입력하면 `merchant_uid`값과 무관하게 환불요청이 실패합니다.

> **환불 금액**(`amount`)
>
> **미입력시 전액이 환불**됩니다.

> **환불 가능 금액**(`checksum`)
>
> 환불이 가능한 금액을 입력합니다. 예를 들어, 10**,**000원짜리 제품의 `checksum`은 10,000입니다. 만약 10,000원짜리 제품이 과거 1,000원 부분환불 되었다면, 이후 환불시 `checksum`은 9,000입니다.입력된 `checksum`을 사용해서 서버와 아임포트 서버간에 환불 가능 금액이 일치하는지 확인합니다. 만약 일치하지 않으면 환불 요청은 실패하며 미 입력시 검증은 실행되지 않습니다.

{% hint style="warning" %}
**checksum을 입력해야 하는 이유**

`checksum`은 필수입력은 아니지만 **서버와 아임포트 서버간에 환불 가능 금액을 검증하기** 위해서 입력을 권장합니다.&#x20;

예를 들어, 10**,**000원짜리 제품에 대한 1,000원 부분환불 요청이 아임포트 서버에서 완료하였으나 가맹점이 서버 혹은 DB오류로 이를 반영하지 못했다면? 아임포트 서버의 checksum은 9,000이 되고, 가맹점 서버의 checksum은 그대로 10,000이 됩니다.&#x20;

이후 남은 금액을 환불하려고 할때 `checksum(10,000)`을 입력하면, 해당 값이 아임포트 서버의 `checksum(9,000)`과 일치하지 않으므로 요청은 실패합니다.
{% endhint %}

#### 아래는 환불 요청을 하는 예제입니다.

{% code title="Node.js" %}
```javascript
/* ... 중략 ... */
  app.post('/payments/cancel', async (req, res, next) => {
    try {
      /* 액세스 토큰(access token) 발급 */
      /* ... 중략 ... */
      /* 결제정보 조회 */
      const { body } = req;
      // 클라이언트로부터 전달받은 주문번호, 환불사유, 환불금액
      const { merchant_uid, reason, cancel_request_amount } = body; 
      Payments.find({ merchant_uid }, async function(err, payment) { 
        /* ... 중략 ... */
        const paymentData = payment[0]; // 조회된 결제정보
        // 조회한 결제정보로부터 imp_uid, amount(결제금액), cancel_amount(환불된 총 금액) 추출
        const { imp_uid, amount, cancel_amount } = paymentData;
        // 환불 가능 금액(= 결제금액 - 환불 된 총 금액) 계산 
        const cancelableAmount = amount - cancel_amount; 
        if (cancelableAmount <= 0) { // 이미 전액 환불된 경우
          return res.status(400).json({ message: "이미 전액환불된 주문입니다." });
        }
        ...
        /* 아임포트 REST API로 결제환불 요청 */
        const getCancelData = await axios({
          url: "https://api.iamport.kr/payments/cancel",
          method: "post",
          headers: {
            "Content-Type": "application/json",
            "Authorization": access_token // 아임포트 서버로부터 발급받은 엑세스 토큰
          },
          data: {
            reason, // 가맹점 클라이언트로부터 받은 환불사유
            imp_uid, // imp_uid를 환불 `unique key`로 입력
            amount: cancel_request_amount, // 가맹점 클라이언트로부터 받은 환불금액
            checksum: cancelableAmount // [권장] 환불 가능 금액 입력
          }
        });
        const { response } = getCancelData.data; // 환불 결과
        /* 환불 결과 동기화 */
        ...
      });
    } catch (error) {
      res.status(400).send(error);
    }
  })
```
{% endcode %}

### <mark style="color:blue;">**STEP 04.**</mark> 환불 결과 저장하기

#### 결제 취소가 완료되면 그 결과를 데이터베이스에 다음과 같이 저장합니다.

{% code title="Node.js" %}
```javascript
/* ... 중략 ... */
  app.post('/payments/cancel', async (req, res, next) => {
    try {
      /* 액세스 토큰(access token) 발급 */
      /* ... 중략 ... */
      /* 결제정보 조회 */
      Payments.find({ merchant_uid }, async function(err, payment) { 
        /* ... 중략 ... */
        /* 아임포트 REST API로 결제환불 요청 */
        /* ... 중략 ... */
        const { response } = getCancelData.data; // 환불 결과
        /* 환불 결과 동기화 */
        const { merchant_uid } = response; // 환불 결과에서 주문정보 추출
        Payments.findOneAndUpdate({ merchant_uid }, response, { new: true }, function(err, payment) { // 주문정보가 일치하는 결제정보를 추출해 동기화
          if (err) {
            return res.json(err);
          }
          res.json(payment); // 가맹점 클라이언트로 환불 결과 반환
        });
      });
    } catch (error) {
      res.status(400).send(error);
    }
  });

```
{% endcode %}

{% hint style="warning" %}
**취소 시 유의할 점**

REST API[**(POST https://api.iamport.kr/payments/cancel)**](../api/api-1/api.md) 요청에 대한 **응답 코드가 200**이라도 응답 body의 code가 0이 아니면 **환불에 실패했다는 의미**입니다. 실패 사유는 body의 message를 통해 확인하셔야 합니다.
{% endhint %}

### <mark style="color:blue;">**STEP 04.**</mark> 환불 응답 처리하기

취소요청에 대한 응답을 클라이언트에게 처리하는 로직을 아래와 같이 작성합니다.

{% tabs %}
{% tab title="HTML" %}
{% code title="client-side" %}
```html
<button onclick="cancelPay()">환불하기</button>
<script
  src="https://code.jquery.com/jquery-3.3.1.min.js"
  integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8="
  crossorigin="anonymous"></script><!-- jQuery CDN --->
<script>
  function cancelPay() {
    jQuery.ajax({
      /* ... 중략 ... */
    }).done(function(result) { // 환불 성공시 로직 
      alert("환불 성공");
    }).fail(function(error) { // 환불 실패시 로직
      alert("환불 실패");
    });
  }
</script>
```
{% endcode %}
{% endtab %}

{% tab title="React.js" %}
{% code title="client-side" %}
```jsx
class CancelPay extends React.Component {
  cancelPay = () => {
    axios({
      /* ... 중략 ... */
    }).then(response => { // 환불 성공시 로직 
      alert("환불 성공");
    }).catch(error => { // 환불 실패시 로직 
      alert("환불 실패");
    });
  }
  ...
  render() {
    return <button onClick={this.cancelPay}>환불하기</button>;
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

---
description: 차이포트 결제취소 API를 이용한 결제취소 방법을 안내합니다.
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

취소 요청을 하기 위해서 먼저 [<mark style="color:blue;">**REST API access token**</mark>](../api/rest-api-access-token/) **** 을 발급받습니다. 발급받은 액세스 토큰(**`access token`**)을 이용하여 [<mark style="color:blue;">**차이포트 취소 API**</mark>](../api/rest-api-access-token/api-2.md) <mark style="color:blue;">****</mark> 를 호출하여 결제 취소를 요청합니다.

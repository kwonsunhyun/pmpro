---
description: PG결제창을 이용한 인증결제를 손쉽게 연동할 수 있습니다.
---

# 🖥 인증결제 연동하기

## 1. 아포트 라이브러리 추가

결제창 연동을 진행할 주문 페이지에 아래 JS 라이브러리를 추가 합니다.

{% hint style="info" %}
**jQuery 1.0** 이상이 설치되어 있어야 합니다.
{% endhint %}

{% code title="client-side" %}
```html
<!-- jQuery -->
<script type="text/javascript" src="https://code.jquery.com/jquery-1.12.4.min.js" ></script>
<!-- iamport.payment.js -->
<script type="text/javascript" src="https://cdn.iamport.kr/js/iamport.payment-{SDK-최신버전}.js"></script>
```
{% endcode %}

## 2. 객체 초기화 하기

#### 주문 페이지에서 [가맹점식별코드](../../undefined/3..md)를 이용하여 IMP 객체를 초기화 합니다.

{% tabs %}
{% tab title="JavaScript" %}
{% code title="Client-side" %}
```javascript
  var IMP = window.IMP;   // 생략 가능
  IMP.init("가맹점식별코드"); // 예: imp00000000 
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (ES Next)" %}
{% code title="Client-side" %}
```javascript
  const IMP = window.IMP; // 생략 가능
  IMP.init("{Merchant ID}"); // Example: imp00000000a
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
해당 초기화 작업을 **1회 이상** 처리되지 않도록 유의하세요
{% endhint %}

## 3. 결제 요청하기

[**IMP 객체 초기화**](2..md) \*\*\*\* 가 완료 되었으면 이제 결제창을 호출할 차례입니다.

결제창 호출시 필요한 [**파라미터**](../../sdk/javascript-sdk/)**를 request\_pay** 함수 첫번째 파라미터 인자로 설정합니다.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
<script>
    function requestPay() {
      IMP.request_pay({ 
          pg: "kcp",
          pay_method: "card",
          merchant_uid: "ORD20180131-0000011",   //주문번호
          name: "노르웨이 회전 의자",
          amount: 64900,                         // 숫자타입
          buyer_email: "gildong@gmail.com",
          buyer_name: "홍길동",
          buyer_tel: "010-4242-4242",
          buyer_addr: "서울특별시 강남구 신사동",
          buyer_postcode: "01181"
      }, function (rsp) { // callback
          if (rsp.success) {
              ...,
              // 결제 성공 시 로직,
              ...
          } else {
              ...,
              // 결제 실패 시 로직,
              ...
          }
      });
    }
  </script>
```
{% endtab %}

{% tab title="React.js" %}
```jsx
class RequestPay extends React.Component {
    requestPay = () => {
      IMP.request_pay({ // param
        pg: "kcp",
        pay_method: "card",
        merchant_uid: "ORD20180131-0000011",
        name: "노르웨이 회전 의자",
        amount: 64900,
        buyer_email: "gildong@gmail.com",
        buyer_name: "홍길동",
        buyer_tel: "010-4242-4242",
        buyer_addr: "서울특별시 강남구 신사동",
        buyer_postcode: "01181"
      }, rsp => { // callback
        if (rsp.success) {
          ...,
          // 결제 성공 시 로직,
          ...
        } else {
          ...,
          // 결제 실패 시 로직,
          ...
        }
      });
    }
```
{% endtab %}

{% tab title="Vue.js" %}
```javascript
<script>
    export default {
      methods: {
        requestPay: function () {
          IMP.request_pay({ // param
            pg: "kcp",
            pay_method: "card",
            merchant_uid: "ORD20180131-0000011",
            name: "노르웨이 회전 의자",
            amount: 64900,
            buyer_email: "gildong@gmail.com",
            buyer_name: "홍길동",
            buyer_tel: "010-4242-4242",
            buyer_addr: "서울특별시 강남구 신사동",
            buyer_postcode: "01181"
          }, rsp => { // callback
            if (rsp.success) {
              ...,
              // 결제 성공 시 로직,
              ...
            } else {
              ...,
              // 결제 실패 시 로직,
              ...
            }
          });
        }
      }
    }
  </script>
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**주문번호(merchant\_uid) 생성 시 유의사항**

* 주문번호는 결제창 요청 시 항상 **고유 값**으로 채번 되어야 합니다.
* 결제 완료 이후 **결제 위변조** 대사 작업시 주문번호를 이용하여 검증이 필요하므로 주문번호는 가맹점 서버에서 고유하게(**unique**)채번하여 **DB 상에 저장**해주세요
{% endhint %}

#### 현재까지 진행한 소스코드에 <mark style="color:red;">결제 취소버튼</mark>을 추가한 샘플코드 입니다.

{% code title="sample.html" %}
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- jQuery -->
    <script type="text/javascript" src="https://code.jquery.com/jquery-1.12.4.min.js" ></script>
    <!-- iamport.payment.js -->
    <script type="text/javascript" src="https://cdn.iamport.kr/js/iamport.payment-1.2.0.js"></script>
    <script>
        var IMP = window.IMP; 
        IMP.init("impXXXXXXXXX"); 

        function requestPay() {
            IMP.request_pay({
                pg : 'kcp',
                pay_method : 'card',
                merchant_uid: "57008833-33004", 
                name : '당근 10kg',
                amount : 1004,
                buyer_email : 'Iamport@chai.finance',
                buyer_name : '아임포트 기술지원팀',
                buyer_tel : '010-1234-5678',
                buyer_addr : '서울특별시 강남구 삼성동',
                buyer_postcode : '123-456'
            }, function (rsp) { // callback
                if (rsp.success) {
                    console.log(rsp);
                } else {
                    console.log(rsp);
                }
            });
        }
    </script>
    <meta charset="UTF-8">
    <title>Sample Payment</title>
</head>
<body>
    <button onclick="requestPay()">결제하기</button> <!-- 결제하기 버튼 생성 -->
</body>
</html>
```
{% endcode %}

## 4-a. 결제결과 처리(iframe)

결제가 정상적으로 완료되면 결제창 형태에 따라 아래와 같이 결제결과를 받아 볼 수 있습니다.

|    iframe 형태    |         팝업형태         |
| :-------------: | :------------------: |
| **callback 함수** | **m\_redirect\_url** |

{% hint style="info" %}
**iframe 이란?**\
\*\*\*\*효과적으로 **다른 HTML 페이지를 현재 페이지에 포함**시키는 중첩된 브라우저로

iframe 요소를 이용하면 해당 웹 페이지 안에 어떠한 제한 없이 **다른 페이지를 불러와서 삽입** 할 수 있습니다.
{% endhint %}

![iframe 예시](<../../.gitbook/assets/image (18) (1) (1) (1) (1) (1).png>)

#### **PC 환경**에서 일어나는 대부분의 결제는 **request\_pay**() 함수 두번째 인자인 **callback** 함수를 통해 결제 결과 수신이 가능합니다.

{% hint style="success" %}
**Paypal** 결제는 PC 환경 결제 시 \*\*팝업형태(새 창)\*\*로 결제창이 활성화 되며

이에따라 결제 결과도 **m\_redirect\_url** 로 받아보실 수 있습니다.
{% endhint %}

> 아래 예제 코드는 결제창 형태가 **iframe 으로 활성화** 되는 **대부분의 PC 환경**에서의 결제요청애 대한 응답을
>
> 처리하는 부분입니다.

{% tabs %}
{% tab title="JavaScript" %}
{% code title="client-side" %}
```javascript
IMP.request_pay({
      /* ...중략... */
    }, function (rsp) {             // callback
      if (rsp.success) {            // 결제 성공 시: 결제 승인 또는 가상계좌 발급에 성공한 경우
        // jQuery로 HTTP 요청
        jQuery.ajax({
            url: "{서버의 결제 정보를 받는 가맹점 endpoint}", 
            method: "POST",
            headers: { "Content-Type": "application/json" },
            data: {
                imp_uid: rsp.imp_uid,            //결제 고유번호     
                merchant_uid: rsp.merchant_uid   //주문번호
            }
        }).done(function (data) {
          // 가맹점 서버 결제 API 성공시 로직
        })
      } else {
        alert("결제에 실패하였습니다. 에러 내용: " +  rsp.error_msg);
      }
    });
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (ES Next)" %}
{% code title="client-side" %}
```javascript
IMP.request_pay({
    /* ...중략... */
  }, rsp => {                      // callback
    if (rsp.success) {   
      // axios로 HTTP 요청
      axios({
        url: "{서버의 결제 정보를 받는 endpoint}",
        method: "post",
        headers: { "Content-Type": "application/json" },
        data: {
          imp_uid: rsp.imp_uid,
          merchant_uid: rsp.merchant_uid
        }
      }).then((data) => {
        // 서버 결제 API 성공시 로직
      })
    } else {
      alert(\`결제에 실패하였습니다. 에러 내용: \${rsp.error_msg}\`);
    }
  });
```
{% endcode %}
{% endtab %}
{% endtabs %}

결제가 완료되면 반환되는 응답 객체([**rsp**](../../sdk/javascript-sdk/))의 결제 성공 여부에 따라 처리 로직을 **callback** 함수에 작성합니다. 요청이 성공했을 경우에 **결제번호(imp\_uid)와 주문번호(merchant\_uid)를 서버에 전달**하는 로직을 위와같이 작성합니다.

> **callback** 함수로 내려가는 응답 파라미터 확인은 [<mark style="color:red;">**여기서**</mark>](../../sdk/javascript-sdk/undefined-1.md) 가능합니다.

{% hint style="danger" %}
최종 결제결과 로직처리는 반드시 [<mark style="color:red;">**웹훅**</mark>](../../undefined-2/webhook.md)을 이용하여 안정적으로 처리해 주셔야 합니다.

웹훅연동을 생략하시는 경우 결제결과를 정상적으로 수신받지 못하는 상황이 발생합니다.
{% endhint %}

## 4-b. 결제결과 처리(redirect)

> 아래 예제 코드는 결제창 형태가 **새로운 페이지로 리디렉션되어** 결제가 진행되는 대부분의 **모바일 환경**에서의 결제요청애 대한 응답을 처리하는 부분입니다.

{% tabs %}
{% tab title="JavaScript" %}
{% code title="client-side" %}
```javascript
IMP.request_pay({
      /* ...중략... */,
      m_redirect_url: "{리디렉션 될 URL}" 
  }, /* callback */);     // callback은 실행 안됨
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (ES Next)" %}
{% code title="client-side" %}
```javascript
IMP.request_pay({
      /* ...중략... */,
      m_redirect_url: "{리디렉션 될 URL}" 
}, /* callback */); // callback은 실행 안됨
```
{% endcode %}
{% endtab %}
{% endtabs %}

위와같이 **request\_pay** 함수 파라미터로 **m\_redirect\_url** 을 설정하면 **결제 완료** 이후 해당 URL 주소로 결제 결과를 **쿼리스트링** 형태로 전송해 드립니다.

아래는 쿼리스트링으로 리디렉션되는 URL 예제입니다.

{% tabs %}
{% tab title="결제완료/가상계좌 발급완료" %}
```url
curl https://myservice.com/payments/complete?imp_uid=결제건을_특정하는_아임포트_번호&merchant_uid=가맹점_고유_주문번호&imp_success=true
```
{% endtab %}

{% tab title="결제 실패" %}
```
curl https://myservice.com/payments/complete?imp_uid=결제건을_특정하는_아임포트_번호&merchant_uid=가맹점_고유_주문번호&imp_success=false&error_code=에러_코드(현재_정리된_체계는_없음)&error_msg=에러_메시지
```
{% endtab %}
{% endtabs %}

|                    파라미터명                    |      설명     |  비고  |
| :-----------------------------------------: | :---------: | :--: |
|                 **imp\_uid**                | 아임포트 결제거래번호 |  공통  |
|              **merchant\_uid**              |   가맹점 주문번호  |  공통  |
|               **imp\_success**              |    결제성공여부   |  공통  |
| <mark style="color:red;">error\_code</mark> |     오류코드    | 실패 시 |
|  <mark style="color:red;">error\_msg</mark> |     오류메세    | 실패 시 |

{% hint style="danger" %}
**결제창이 리디렉션되어 새로운 페이지에서 활성화되는 경우 결제 결과는 callback 으로 받을 수 없습니다.**
{% endhint %}

> **결제 완료의 의미**
>
> `결제완료`는 아래의 모든 경우를 포함합니다.
>
> 1. **결제 성공**(결제 상태: `paid`, imp\_success: `true`)
> 2. **결제 실패**(결제 상태: `failed`, imp\_success: `false`)
> 3. PG 모듈 설정이 올바르지 않아, **결제 창이 열리지 않음**
> 4. 사용자가 임의로 X 버튼이나 취소 버튼을 눌러 **결제를 종료**함
> 5. 카드 정보 불일치, 한도 초과, 잔액 부족 등의 사유로 **결제가 중단**됨
> 6. 가상계좌 \*\*발급 완료(\*\*결제 상태: `ready`, imp\_success: `true`)

{% hint style="danger" %}
최종 결제결과 로직처리는 반드시 [<mark style="color:red;">**웹훅**</mark>](../../undefined-2/webhook.md)을 이용하여 안정적으로 처리해 주셔야 합니다.

웹훅연동을 생략하시는 경우 결제결과를 정상적으로 수신받지 못하는 상황이 발생합니다.
{% endhint %}

## 5. 결제정보 검증하기

운영중인 서버에서 클라이언트로 부터 전달 받은 결제 결과 데이터를 바탕으로 <mark style="color:red;">**결제금액 위변조 여부**</mark>를 검증하고 필요시 데이터베이스에 저장합니다. 결제 정보를 검증하는 과정은 크게 아래와 같은 단계로 진행합니다.

* 아임포트 결제고유번호(**imp\_uid**), 주문번호(**merchant\_uid**)를 서버단에서 수신
* 결제 상세내역 조회를 위해 아임포트 [**결제 단건 조회 API** ](https://api.iamport.kr/#!/payments/getPaymentByImpUid)요청
* 응답받은 내용을 바탕으로 실 결제 금액과 결제요청금액(가맹점 자체 데이터베이스)을 비교

### <mark style="color:green;">**STEP 01**</mark> 결제결과 서버 수신

{% tabs %}
{% tab title="Node.js" %}
결제정보를 받은 가맹점 endpoint URL 에 대한 POST 요청을 수신하는 예제

{% code title="server-side" %}
```javascript
app.use(bodyParser.json());
  // "{서버의 결제 정보를 받는 가맹점 endpoint}" POST 요청 수신부
  app.post("/payments/complete", async (req, res) => {
    try {
      // req의 body에서 imp_uid, merchant_uid 추출
      const { imp_uid, merchant_uid } = req.body; 
    } catch (e) {
      res.status(400).send(e);
    }
  });
```
{% endcode %}
{% endtab %}
{% endtabs %}

### <mark style="color:green;">**STEP 02**</mark> 결제내역 단건 조회

{% tabs %}
{% tab title="Node.js" %}
수신받은 아임포트 \*\*결제고유번호(imp\_uid)\*\*로 [**결제단건조회**](https://api.iamport.kr/#!/payments/getPaymentByImpUid) **API** 를 호출하여 결제정보 획득 예제

{% code title="server-side" %}
```javascript
app.use(bodyParser.json());
    ...
    app.post("/payments/complete", async (req, res) => {
      try {
        // req의 body에서 imp_uid, merchant_uid 추출
        const { imp_uid, merchant_uid } = req.body; 
        ...
        // 액세스 토큰(access token) 발급 받기
        const getToken = await axios({
          url: "https://api.iamport.kr/users/getToken",
          method: "post", // POST method
          headers: { "Content-Type": "application/json" }, 
          data: {
            imp_key: "imp_apikey", // REST API 키
            imp_secret: "ekKoeW8RyKuT0zgaZsUtXXTLQ4AhPFW3ZGseDA6bkA5lamv9OqDMnxyeB9wqOsuO9W3Mx9YSJ4dTqJ3f" // REST API Secret
          }
        });
        const { access_token } = getToken.data.response; // 인증 토큰
        ...
        // imp_uid로 아임포트 서버에서 결제 정보 조회
        const getPaymentData = await axios({
          // imp_uid 전달
          url: \`https://api.iamport.kr/payments/\${imp_uid}\`, 
          // GET method
          method: "get", 
          // 인증 토큰 Authorization header에 추가
          headers: { "Authorization": access_token } 
        });
        const paymentData = getPaymentData.data.response; // 조회한 결제 정보
        ...
      } catch (e) {
        res.status(400).send(e);
      }
    });
```
{% endcode %}
{% endtab %}
{% endtabs %}

### <mark style="color:green;">**STEP 03**</mark> 결제정보 검증

> **결제금액의 위변조 검증 이유**
>
> 결제 요청은 클라이언트 환경에서 이루어지기 때문에 **클라이언트 스크립트를 조작해 금액을 위 변조하여 결제를 요청**할 수 있습니다. 따라서 결제완료 후 처음 요청했던 금액과 실제로 결제된 금액을 반드시 비교해야 합니다.
>
> 예를 들어, 100,000원짜리 상품을 결제할 때에는 `amount: 100000`으로 결제요청을 하게 되는데, 공격자가 스크립트를 조작하여 해당 속성을 실제 금액보다 낮은 값으로 변조할 수 있습니다.
>
> 클라이언트에서의 스크립트 조작은 원천적으로 막을 수 없는 기술적 특징이 있기 때문에 **결제 후 서버에서 결제금액의 위변조 여부를 반드시 검증**해야 합니다.

{% tabs %}
{% tab title="Node.js" %}
결제된 실 금액과 요청 금액을 비교하여 **결제금액 위변조여부 검증** 및 DB저장 예시

{% code title="server-side" %}
```javascript
app.use(bodyParser.json());
  ...
  app.post("/payments/complete", async (req, res) => {
    try {
      // req의 body에서 imp_uid, merchant_uid 추출
      const { imp_uid, merchant_uid } = req.body; 
      // 액세스 토큰(access token) 발급 받기
      /* ...중략... */
      // imp_uid로 아임포트 서버에서 결제 정보 조회
      /* ...중략... */
      const paymentData = getPaymentData.data.response; // 조회한 결제 정보
      ...
      // DB에서 결제되어야 하는 금액 조회
      const order = await Orders.findById(paymentData.merchant_uid);
      const amountToBePaid = order.amount; // 결제 되어야 하는 금액
      ...
      // 결제 검증하기
      const { amount, status } = paymentData;
      // 결제금액 일치. 결제 된 금액 === 결제 되어야 하는 금액
      if (amount === amountToBePaid) { 
        await Orders.findByIdAndUpdate(merchant_uid, { $set: paymentData }); // DB에 결제 정보 저장
        ...
        switch (status) {
          case "ready": // 가상계좌 발급
            // DB에 가상계좌 발급 정보 저장
            const { vbank_num, vbank_date, vbank_name } = paymentData;
            await Users.findByIdAndUpdate("/* 고객 id */", { $set: { vbank_num, vbank_date, vbank_name }});
            // 가상계좌 발급 안내 문자메시지 발송
            SMS.send({ text: \`가상계좌 발급이 성공되었습니다. 계좌 정보 \${vbank_num} \${vbank_date} \${vbank_name}\`});
            res.send({ status: "vbankIssued", message: "가상계좌 발급 성공" });
            break;
          case "paid": // 결제 완료
            res.send({ status: "success", message: "일반 결제 성공" });
            break;
        }
      } else { // 결제금액 불일치. 위/변조 된 결제
        throw { status: "forgery", message: "위조된 결제시도" };
      }
    } catch (e) {
      res.status(400).send(e);
    }
  });
```
{% endcode %}
{% endtab %}
{% endtabs %}

처음 요청한 금액은 **`merchant_uid`** 로 데이터베이스에서 조회하고 실제 결제금액은 **`imp_uid`로 아임포트 서버에서 조회하여 두 값을 비교합니다. 검증이 성공하면 결제 정보를 데이터베이스에 저장한 뒤 결제 상태(`status`**)에 따라 알맞은 응답을 반환하고 실패 시 에러 메세지를 출력합니다.

{% hint style="danger" %}
결제결과 DB 처리는 \*\*웹훅(Webhook)\*\*을 연동하여 수신되는 데이터를 기준으로 처리하셔야 결제결과 누락없이 안정적인 결과처리를 완료하실 수 있습니다.
{% endhint %}

## 6. 결제완료 처리하기

**Iframe** 방식으로 진행되는 대부분의 PC환경 결제인 경우 결제응답은 **callback** 함수로 받아볼 수 있으며 가맹점 서버에서 결제결과 처리가 최종적으로 완료되면 아래 예제처럼 결제 성공유무에 따른 분기를 통해 결과 메세지 처리를 진행 하실 수 있습니다.

{% tabs %}
{% tab title="JavaScript" %}
{% code title="client-side" %}
```javascript
IMP.request_pay({
    /* ...중략... */
  }, function (rsp) { // callback
    if (rsp.success) { // 결제 성공 시: 결제 승인 또는 가상계좌 발급에 성공한 경우
        // jQuery로 HTTP 요청
        jQuery.ajax({
          /* ...중략... */
        }).done(function(data) { // 응답 처리
          switch(data.status) {
            case: "vbankIssued":
              // 가상계좌 발급 시 로직
              break;
            case: "success":
              // 결제 성공 시 로직
              break;
          }
        });
    } else {
      alert("결제에 실패하였습니다. 에러 내용: " +  rsp.error_msg);
    }
  });
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (ES Next)" %}
{% code title="client-side" %}
```javascript
IMP.request_pay({
    /* ...중략... */
  }, rsp => { // callback
    if (rsp.success) { // 결제 성공 시: 결제 승인 또는 가상계좌 발급에 성공한 경우
      // axios로 HTTP 요청
      axios({
        /* ...중략... */
      }).then((data) => { // 응답 처리
        switch(data.status) {
          case: "vbankIssued":
            // 가상계좌 발급 시 로직
            break;
          case: "success":
            // 결제 성공 시 로직
            break;
        }
      });
    } else {
      alert(\`결제에 실패하였습니다. 에러 내용: \${rsp.error_msg}\`);
    }
  });
```
{% endcode %}
{% endtab %}
{% endtabs %}

새로운 페이지로 리디렉션되어 결제가 진행되는 대부분의 **모바일환경**에서의 결제는 **m\_redirect\_url** 파라미터로 설정하신 가맹점 **EndPoint URL 에서 최종 결제완료 메세지 처리**를 진행해 주시면 됩니다.

{% hint style="info" %}
**error\_msg, error\_code 정의**

결제 실패 시 응답으로 내려가는 해당 파라미터는 원천사(PG사)에서 내려주 오류코드와 메세지를 2차 가공없이 \*\*\*\* 그대로 내려드리고 있습니다. 이에 따라 현재 취합된 오류코드와 오류메세지 정의문서는 아직 지원해 드리고 있지 않은점 참고해주세요
{% endhint %}

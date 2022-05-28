---
description: 웹훅 연동을 통해 결제 결과를 안전하게 처리하실 수 있습니다.
---

# ⚒ 웹훅(Webhook) 연동하기

아임포트 **웹훅**(webhook)을 사용하여 아임포트 서버에 저장된 결제 정보를 가맹점 서버에 동기화하고 네트워크 불안정성을 보완하는 방법을 설명합니다.

{% hint style="info" %}
**웹훅(Webhook)이란?**

특정 이벤트가 발생하였을 때 타 서비스나 응용프로그램으로 알림을 보내는 기능입니다. Webhook 프로바이더는 해당 이벤트가 발행하면 `HTTP POST` 요청을 생성하여 callback URL(endpoint)로 이벤트 정보을 보냅니다. 주기적으로 데이터를 폴링(polling)하지 않고 원하는 이벤트에 대한 정보만 수신할 수 있어서 webhook은 리소스나 통신측면에서 훨씬 더 효율적입니다. Webhook을 활용하면 커스텀기능이나 다른 애플리케이션과 연동하여 기능을 확장할 수 있습니다.
{% endhint %}

{% hint style="success" %}
**웹훅(Webhook) 연동은 필수 인가요?**

아임포트 서버에서 클라이언트 응답을 전달할 때 Wi-Fi 연결 끊김, 혹은 브라우저 자동 리로드 등의 이유로 클라이언트에서 결제 완료에 대한 응답을 받지 못하는 경우가 간헐적으로 발생합니다. 이런 경우를 대비해서 아임포트 서버에서 가맹점 서버로 webhook 이벤트를 발송하여 결제 정보를 동기화할 수 있도록 합니다.
{% endhint %}

아임포트 웹훅(webhook)은 다음과 같은 경우에 호출됩니다.

> * **결제가 승인**되었을 때(모든 결제 수단) - (status : `paid`)
> * **가상계좌가 발급**되었을 때 - (status : `ready`)
> * **가상계좌에 결제 금액이 입금**되었을 때 - (status : `paid`)
> * **예약결제가 시도**되었을 때 - (status : `paid` or `failed`)
> * **관리자 콘솔에서 결제 취소**되었을 때 - (status : `cancelled`)

{% hint style="danger" %}
**결제 실패 시에는 웹훅이 호출되지 않아요!**
{% endhint %}

웹훅(Webhook)수신을 위한 URL 설정은 두가지 형태로 지원됩니다.

{% tabs %}
{% tab title="관리자콘솔 설정" %}
![웹훅 URL 설정방법](<../.gitbook/assets/image (6) (1) (1) (1) (1).png>)

아임포트 webhook이 호출될 때 결제 정보를 통보받을 URL을 설정하려면 아임포트 관리자 콘솔 내 [시스템설정 페이지 > 웹훅(Notification)설정](https://admin.iamport.kr/settings#tab\_webhook) 탭을 선택합니다. 상단의 **웹훅(Notification)발송 공통 URL**란에 전 단계에서 복사한 값을 입력하고, 하단의 **웹훅설정 저장** 버튼을 눌러 설정을 저장합니다.

**Content-Type** 은 `application/json` 또는 `application/x-www-form-urlencoded`으로 지정할 수 있습니다. 필드 우측의 **호출 테스트** 버튼을 누르면 해당 URL을 호출하여 테스트할 수 있습니다
{% endtab %}

{% tab title="파라미터 설정" %}
JavaScript SDK **request\_pay** 함수 요청시 <mark style="color:blue;">**notice\_url**</mark> 파라미터를 사용하시면 설정하신 URL로 웹훅을 전송해 드립니다. 매 결제 요청시 웹훅주소를 상이하게 운영하고 싶은 경우 사용합니다.

(해당 파라미터 설정시 관리자 콘솔 <mark style="color:red;">**웹훅 설정은 무시**</mark>됩니다.)

{% code title="client-side" %}
```javascript
function requestPay() {
    // IMP.request_pay(param, callback) 결제창 호출
    IMP.request_pay({
        ...            //중
        notice_url : 'https://웹훅수신 URL',   //웹훅수신 URL 설
        ...            //중
    }, function (rsp) { // callback
        if (rsp.success) {
            console.log(rsp);
        } else {
            console.log(rsp);
        }
    });
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**웹훅(Webhook) URL 복수개 설정은 지원되지 않습니다.**
{% endhint %}

### 웹훅(Webhook) 요청 검증하기 <a href="#webhook" id="webhook"></a>

웹훅 수신주소는 공개된 URL이기 때문에 **요청자 클라이언트(client IP)가 아임포트(Iamport IP)인지 반드시 확인**해야 합니다. 아임포트 웹훅은 다음의 두 가지 **고정된 IP** 로 부터 요청이 생성됩니다.

> * <mark style="color:red;">**52.78.100.19**</mark>
> * <mark style="color:red;">**52.78.48.223**</mark>

웹훅(Webhook) 이벤트가 호출되면 설정한 URL endpoint에 대해 다음과 같은 `POST` 요청이 생성됩니다.

{% tabs %}
{% tab title="cURL" %}
```url
curl -H "Content-Type: application/json" -X POST -d '{ "imp_uid": "imp_1234567890", "merchant_uid": "order_id_8237352", "status": "paid" }' { NotificationURL }
```
{% endtab %}
{% endtabs %}

> Webhook `POST` 요청의 본문은 다음의 정보를 포함합니다. 가맹점 서버는 해당 정보를 수신하고 아임포트 서버에서 결제 정보를 조회하여 검증 및 저장할 수 있습니다.
>
> * <mark style="color:red;">**`imp_uid`**</mark><mark style="color:red;">**: 결제번호**</mark>
> * <mark style="color:red;">**`merchant_uid`**</mark><mark style="color:red;">**: 주문번호**</mark>
> * <mark style="color:red;">**`status`**</mark><mark style="color:red;">**: 결제 결과**</mark>

웹훅 EndPoint URL 수신부 POST 요청에 대한 코드 예시

{% tabs %}
{% tab title="Node.js" %}
Webhook 이벤트의 `POST` 요청을 처리할 endpoint를 다음과 같이 생성하여 결제 정보를 조회하고 검증하여 저장합니다.

{% code title="server-side" %}
```javascript
app.use(bodyParser.json());
  ...
  // "/iamport-webhook"에 대한 POST 요청을 처리
  app.post("/iamport-webhook", async (req, res) => {
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
          // DB에 결제 정보 저장
          await Orders.findByIdAndUpdate(merchant_uid, { $set: paymentData }); 
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

{% hint style="danger" %}
**서버가 결제 정보를 수신 하는 순서는 보장되지 않습니다**

기본적으로 아임포트 서버에서 webhook이 호출되면 가맹점 응답을 기다리지 않고 클라이언트에 302 redirect 응답을 보내기 때문에 결과 도달에 대한 순서를 보장하지 않습니다. 다만 가맹점 요청이 있을 경우 webhook 호출이후에 클라이언트에 302 redirect 또는 callback 응답을 보내어 순서를 보장 해드리고 있습니다. 여기서 주의할 점은 웹훅 요청에 대한 가맹점 응답과 무관하게 아임포트는 웹훅발송 이후 바로 클라이언트로 응답(**Callback or Redirect**)을 내리는 부분 참고 하셔야 합니다.

웹훅 우선순위 요청은 [support@iamport.kr](mailto:support@iamport.kr) 로 가맹점 식별코드를 기재하여 요청해 주시면 됩니다.
{% endhint %}

{% hint style="info" %}
**웹훅 재 전송이 가능한가요?**

웹훅은 1회 전송이 기본설정입니다. 단 가맹점 요청시 최대 5회까지 재 전송이 가능합니다. 이 경우 1분 간격으로 가맹점 성공응답을 수신할때까지 웹훅이 발송됩니다.(**최대 5회**)
{% endhint %}

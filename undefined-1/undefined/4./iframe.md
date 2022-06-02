---
description: 대부분의 PC환경에서 적용되는 iframe 방식 결제창 환경에서의 결과처리 방법을 안내합니다.
---

# 🪟 iframe 결제창 결과처리

{% hint style="info" %}
**iframe 이란?**\
효과적으로 **다른 HTML 페이지를 현재 페이지에 포함**시키는 중첩된 브라우저로

iframe 요소를 이용하면 해당 웹 페이지 안에 어떠한 제한 없이 **다른 페이지를 불러와서 삽입** 할 수 있습니다.
{% endhint %}

![iframe 예시](<../../../.gitbook/assets/image (18) (1) (1) (1) (1) (1) (1) (1).png>)

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

결제가 완료되면 반환되는 응답 객체([**rsp**](../../../sdk/javascript-sdk/))의 결제 성공 여부에 따라 처리 로직을 **callback** 함수에 작성합니다. 요청이 성공했을 경우에 **결제번호(imp\_uid)와 주문번호(merchant\_uid)를 서버에 전달**하는 로직을 위와같이 작성합니다.

> callback 함수로 내려가는 응답 파라미터 확인은 [<mark style="color:red;">**여기서**</mark>](../../../sdk/javascript-sdk/undefined-1.md) 가능합니다.

{% hint style="danger" %}
최종 결제결과 로직처리는 반드시 [<mark style="color:red;">**웹훅**</mark>](../../../undefined-2/webhook.md)을 이용하여 안정적으로 처리해 주셔야 합니다.

웹훅연동을 생략하시는 경우 결제결과를 정상적으로 수신받지 못하는 상황이 발생합니다.
{% endhint %}

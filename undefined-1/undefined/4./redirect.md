---
description: 새로운창으로 리디렉션되어 결제가 진행되는 환경에서의 결과 처리 방법을 안내합니다.
---

# 🖼 redirect 결제창 결과처리

> 아래 예제 코드는 결제창 형태가 **새로운페이지로 리디렉션되어** 결제가 진행되는 대부분의 **모바일 환경**에서의 결제요청애 대한 응답을 처리하는 부분입니다.

{% content-ref url="../../../tip/redirect.md" %}
[redirect.md](../../../tip/redirect.md)
{% endcontent-ref %}

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

위와같이 **request\_pay** 함수 파라미터로 **m\_redirect\_url** 을 설정하면 <mark style="color:blue;">**결제 완료**</mark> 이후 해당 URL 주소로 결제 결과를 **쿼리스트링(Query String)** 형태로 전송해 드립니다.

{% hint style="info" %}
**Query String 이란?**

URL 뒤에 데이터를 전달하는 가장 단순한 방법으로 주로 GET방식으로 데이터를 전송할때 사용하는 방법입니다.
{% endhint %}

{% swagger method="get" path="complete" baseUrl="https://가맹점 도메인주소/" summary="결제결과를 수신받을 endpoint url 주소를 m_redirect_url 에 설정하시면 결제결과 수신이 가능합니다." %}
{% swagger-description %}
아래 파라미터를 설정하신 URL 을 통해 Query String 형태로 수신받을수 있습니다.
{% endswagger-description %}

{% swagger-parameter in="query" name="imp_uid" required="true" %}
아임포트 결제 고유번호
{% endswagger-parameter %}

{% swagger-parameter in="query" required="true" name="merchant_uid" %}
가맹점 주문번호
{% endswagger-parameter %}

{% swagger-parameter in="query" required="true" name="imp_success" %}

{% endswagger-parameter %}

{% swagger-parameter in="query" name="error_code" required="false" %}
실패코드(결제 실패인 경우 수신)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="error_msg" required="false" %}
실패메세지(결제 실패인 경우 수신)
{% endswagger-parameter %}
{% endswagger %}

아래는 Query String 으로 리디렉션되는 URL 예제입니다.

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

{% hint style="danger" %}
**결제창이 리디렉션되어 새로운 페이지에서 활성화되는 경우 결제 결과는 callback 으로 받을 수 없습니다.**
{% endhint %}

{% hint style="danger" %}
최종 결제결과 로직처리는 반드시 [<mark style="color:red;">**웹훅**</mark>](../../../result/webhook.md)을 이용하여 안정적으로 처리해 주셔야 합니다.

웹훅연동을 생략하시는 경우 결제결과를 정상적으로 수신받지 못하는 상황이 발생합니다.
{% endhint %}

> <mark style="color:blue;">**결제 완료**</mark>**의 의미**
>
> `결제완료`는 아래의 모든 경우를 포함합니다.
>
> 1. **결제 성공**(결제 상태: `paid`, imp\_success: `true`)
> 2. **결제 실패**(결제 상태: `failed`, imp\_success: `false`)
> 3. PG 모듈 설정이 올바르지 않아, **결제 창이 열리지 않음**
> 4. 사용자가 임의로 X 버튼이나 취소 버튼을 눌러 **결제를 종료**함
> 5. 카드 정보 불일치, 한도 초과, 잔액 부족 등의 사유로 **결제가 중단**됨
> 6. 가상계좌 \*\*발급 완료(\*\*결제 상태: `ready`, imp\_success: `true`)

{% hint style="warning" %}
**imp\_success 파라미터**

<mark style="color:red;">`imp_success`</mark> 파라미터는 **결제 프로세스 정상 종료 여부**를 의미합니다. 하지만 클라이언트 상에서 자바스크립트 함수를 호출해서 결제창이 열리므로 **결제금액이 위변조 되었을 가능성**이 있기 때문에 **이 값으로 결제의 성공 여부를 판단해서는 안됩니다**. 결제의 성공 여부에 따라 아래와 같이 처리합니다.

* imp\_success = true: 결제 정보(imp\_uid, merchant\_uid)를 서버에 전달 해서 결제금액의 위변조 여부를 검증한 후 최종적으로 결제 성공 여부를 판단합니다.
* Imp\_success = false: 결제가 실패했음을 사용자에게 알립니다.

\* 일부 PG사에 한해 `imp_success`가 아닌 `success` 파라미터가 전달되거나 아예 전달되지 않는 경우(예: KG이니시스 - 실시간 계좌이체)도 있으니 주의하셔야 합니다.
{% endhint %}

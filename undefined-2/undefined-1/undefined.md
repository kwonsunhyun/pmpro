---
description: 통합인증 연동을 시작하기 위한 준비작업을 소개합니다.
---

# 📒 통합인증 준비하기

### 통합인증을 연동할 페이지에 아임포트 라이브러리를 추가합니다.&#x20;

{% hint style="info" %}
신용카드 본인인증 기능은 **아임포트 JavaScript v1.1.8**부터 지원합니다.
{% endhint %}

{% tabs %}
{% tab title="HTML" %}
{% code title="client-side" %}
```html
<!-- jQuery -->
<script type="text/javascript" src="https://code.jquery.com/jquery-1.12.4.min.js" ></script>
<!-- iamport.payment.js -->
<script type="text/javascript" src="https://cdn.iamport.kr/js/iamport.payment-{SDK-최신버전}.js"></script>
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="danger" %}
**jQuery 1.0 이상이 설치**되어 있어야 합니다.
{% endhint %}

### 본인인증 페이지에 [<mark style="color:blue;">`가맹점 식별코드`</mark>](../../undefined/3..md)를 이용하여 `IMP` 객체를 초기화합니다.

{% tabs %}
{% tab title="JavaScript" %}
{% code title="client-side" %}
```javascript
var IMP = window.IMP; // 생략 가능
IMP.init("{가맹점 식별코드}"); // 예: imp00000000
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript(ES Next)" %}
{% code title="Client-side" %}
```javascript
var IMP = window.IMP; // 생략 가능
IMP.init("{가맹점 식별코드}"); // 예: imp00000000
```
{% endcode %}
{% endtab %}
{% endtabs %}

---
description: 결제창 연동시 호출 및 응답 파라미터를 확인 할 수 있습니다.
---

# 📚 Javascript SDK

아임포트 JavaScript SDK를 사용하면 웹사이트 또는 앱에서 결제창 또는 본인인증창과 연동할 수 있습니다.

버전 내역 및 각 버전의 주요 변경 사항은 [**릴리스 노트**](sdk-release-note.md)를 참조하세요.

### SDK Library 로드하기 <a href="#sdk-library" id="sdk-library"></a>

**아임포트 JavaScript SDK**를 사용하기 위해서 먼저 해당 라이브러리를 다음과 같이 페이지에 추가해야 합니다. 해당 라이브러리는 CDN([https://cdn.iamport.kr/js/iamport.payment-{SDK-최신버전}.js)을](https://cdn.iamport.kr/js/iamport.payment-%7BSDK-%EC%B5%9C%EC%8B%A0%EB%B2%84%EC%A0%84%7D.js\)%EC%9D%84) 통한 사용을 권장합니다. 라이브러리가 로드되면, **IMP** 전역 객체를 **window** 객체의 프로퍼티로 접근하여 **IMP**의 함수들을 호출할 수 있습니다.

{% code title="HTML" %}
```html
<!-- jQuery -->
<script type="text/javascript" src="https://code.jquery.com/jquery-1.12.4.min.js" ></script>
<!-- iamport.payment.js -->
<script type="text/javascript" src="https://cdn.iamport.kr/js/iamport.payment-{SDK-최신버전}.js"></script>
```
{% endcode %}

{% hint style="warning" %}
**jQuery 1.0 이상이 설치**되어 있어야 합니다.
{% endhint %}

> #### **CDN** 사용에 대한 불편함이 있으신 경우 아래 URL 로 설정해 주셔도 무방합니다. [https://service.iamport.kr/js/iamport.payment-](https://service.iamport.kr/js/iamport.payment-1.2.0.js){SDK-최신버전}[.js](https://service.iamport.kr/js/iamport.payment-1.2.0.js)

{% content-ref url="undefined.md" %}
[undefined.md](undefined.md)
{% endcontent-ref %}

{% content-ref url="undefined-1.md" %}
[undefined-1.md](undefined-1.md)
{% endcontent-ref %}

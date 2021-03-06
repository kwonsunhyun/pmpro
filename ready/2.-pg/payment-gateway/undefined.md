---
description: 토스페이먼츠 설정방법을 안내합니다.
---

# ⌨ 토스페이먼츠 설정

## 인증**결제**

{% tabs %}
{% tab title="테스트 결제" %}
### 테스트 환경 구성방법

1. [아임포트관리자콘솔](https://https/admin.iamport.kr) **-> 결제연동 -> 테스트 연동관리 -> 토스페이먼츠 -> **<mark style="color:red;">**(구)토스페이먼츠**</mark>** ->추가**
2. **자동으로 설정된 테스트 MID 확인후 저장 선**

![결제연동 -> 테스트 연동관리 -> 토스페이먼츠 -> (구)토스페이먼츠 ->추가](<../../../.gitbook/assets/image (2) (2).png>)

![자동으로 설정된 테스트 MID 확인후 저장](<../../../.gitbook/assets/image (4) (2).png>)

{% hint style="info" %}
**토스페이먼츠 인증 결제 안내**

아임포트에서 제공하는 토스페이먼츠 인증결제 방식은 **구 모듈** 연동 방식이며 추후 신 모듈로 변경될 예정입니다. 연동하는 가맹점 입장에서는 구모듈과 신모듈의 서비스 차이점은 존재하지 않습니다.&#x20;
{% endhint %}
{% endtab %}

{% tab title="실 결제" %}
### **실** 환경 구성방법

1. **결제연동** -> **실 연동관리** 선택
2. **토스페이먼츠** -> <mark style="color:red;">**토스페이먼츠**</mark> 선택 -> **추가**
3. 토스페이먼츠와 계약 후 발급된 연동상점정보(MID/ MertKey)를 기재합니다.

{% hint style="danger" %}
발급 MID 방식

아임포트를 통한 토스페이먼츠 인증결제를 위해서는 토스페이먼츠 인증결제 MID 발급 요청시 반드시 <mark style="color:red;">**구 인증 모듈 방식**</mark>이라고 언급해주셔야 올바른 값을 부여받을 수 있습니다.
{% endhint %}

![결제연동 -> 실 연동관리 선택](<../../../.gitbook/assets/image (42).png>)

![토스페이먼츠 -> 토스페이먼츠 선택 -> 추가](<../../../.gitbook/assets/image (5).png>)

![토스페이먼츠와 계약 후 발급된 연동상점정보 기재](<../../../.gitbook/assets/image (3) (2).png>)
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**비 인증 결제**

토스페이먼츠 비인증 결제를 이용하기 위해서는 [**아임포트 관리자페이지 가입**](https://https/admin.iamport.kr)이후 **계정ID**(Email 주소)를 cs@iamport.kr 로 신청해주시면 당사에서 설정이후 안내 해 드립니다.
{% endhint %}

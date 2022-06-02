---
description: 차이 간편결제 설정 방법을 안내합니다.
---

# ⌨ 차이 설정

#### 차이 결제 테스트를 위해서는 아래 애플리케이션을 다운로드 받으셔야 합니다.

> * Android : [https://appdistribution.firebase.dev/i/8fef29de1f667252](https://appdistribution.firebase.dev/i/8fef29de1f667252)◦
>
> &#x20;      \- **staging 앱**을 설치
>
> * iOS : [https://testflight.apple.com/join/ZgQIFce5](https://testflight.apple.com/join/ZgQIFce5)
>
> &#x20;     \- 아이폰 설정 > 차이 > 디버그(dev) 모드 활성화 ON
>
> &#x20;     \- 앱의 오른쪽 엣지에서 왼쪽으로 swipe 후 **staging 설정**

{% hint style="info" %}
**테스트 계좌 안내**&#x20;

<mark style="color:red;">**정상 응답 계좌**</mark>

* 국민은행  :  201602181111
* 우리은행  :  201602182222
* 경남은행  :  201602183333

<mark style="color:red;">**잔액 부족 계좌**</mark>

* 국민은행  :  772210258507 &#x20;
* 신한은행  :  110438106449 &#x20;
* 경남은행  :  629220095451 &#x20;
{% endhint %}

## 일반 결제

{% tabs %}
{% tab title="테스트 결제" %}
### 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(**일반결제 및 정기결제**) → PG사 \[간편결제] 차이 선택 → <mark style="color:red;">**테스트모드 \[ON]**</mark> → public\_api\_key 및 private\_api\_key에 발급받은 키 정보 입력 > \[전체 저장] 클릭

>
{% endtab %}

{% tab title="실 결제" %}

{% endtab %}
{% endtabs %}


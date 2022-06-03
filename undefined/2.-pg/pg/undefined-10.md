---
description: 페이팔 설정 방법을 안내합니다.
---

# ⌨ 페이팔 설정

## 인증결제

{% tabs %}
{% tab title="테스트 결제" %}
### 테스트 환경 구성방법



> 페이팔 테스트 환경 구성을 위해서는 **아임포트 관리자 페이지 설정**과 **페이팔 관리자페이지 설정**이 각각 적용되어야 합니다.



**<아임포트 관리자 콘솔 설정 >**

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(**일반결제 및 정기결제**) → PG사 페이팔-Express Checkout 선택 → <mark style="color:red;">**테스트모드 \[ON]**</mark> → API 사용자 정보 입력 → \[전체 저장] 클릭



![](<../../../.gitbook/assets/image (11).png>)

{% hint style="danger" %}
**Email 계정주소 설정시 주의사항**&#x20;

자동완성된 Email 주소가 **실제 페이팔 계정 ID와 상이한 경우** <mark style="color:red;">**실 계정 ID 로 수정**</mark>하여 저장해야 합니다.
{% endhint %}

****

**<페이 관리자 콘솔 설정 >**

#### **판매자 Sandbox 계정 설정**&#x20;

1. &#x20;[https://developer.paypal.com/developer/accounts/](https://developer.paypal.com/developer/accounts/) 로그인 > **SANDBOX** > **Accounts** > DEFAULT Business 계정의 \[**View/edit account**] 클릭

![Accounts 예](<../../../.gitbook/assets/image (19).png>)

**2. Account details 팝업창**

&#x20;API Credentials 탭의 Username, Password, 및 Signature 값을 아임포트 관리자 콘솔 페이팔 설정 항목에 아래와 같이 맵핑합니다.

* Username = API 사용자 이름
* Password = API 암호&#x20;
* Signature = 서명&#x20;

![API Credentials](<../../../.gitbook/assets/image (21).png>)
{% endtab %}

{% tab title="실 결제" %}

{% endtab %}
{% endtabs %}


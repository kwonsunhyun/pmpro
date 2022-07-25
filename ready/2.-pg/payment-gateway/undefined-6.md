---
description: 페이팔 설정 방법을 안내합니다.
---

# ⌨ 페이팔 설정

## 인증결제

{% tabs %}
{% tab title="테스트 결제" %}
### 테스트 환경 구성방법



> * 페이팔 테스트 환경 구성을 위해서는 **아임포트 관리자 페이지 설정**과 **페이팔 관리자페이지 설정**이 각각 적용되어야 합니다.
> * 페이팔은 별도의 계약없이 판매자 계정만 생성하면 바로 서비스 이용이 가능합니다.



### **<아임포트 관리자 콘솔 설정 >**

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(**일반결제 및 정기결제**) → PG사 페이팔-Express Checkout 선택 → <mark style="color:red;">**테스트모드 \[ON]**</mark> → API 사용자 정보 입력 → \[전체 저장] 클릭



![](<../../../.gitbook/assets/image (11) (1) (1) (1) (1).png>)

{% hint style="danger" %}
**Email 계정주소 설정시 주의사항**&#x20;

자동완성된 Email 주소가 **실제 페이팔 계정 ID와 상이한 경우** <mark style="color:red;">**실 계정 ID 로 수정**</mark>하여 저장해야 합니다.
{% endhint %}

****

### **<페이팔 관리자 콘솔 설정 >**

#### <mark style="color:purple;">**판매자 Sandbox 계정 설정**</mark>&#x20;

1. &#x20;[https://developer.paypal.com/developer/accounts/](https://developer.paypal.com/developer/accounts/) 로그인 > **SANDBOX** > **Accounts** > DEFAULT Business 계정의 \[**View/edit account**] 클릭

![Accounts 예](<../../../.gitbook/assets/image (19) (1) (1) (1).png>)

&#x20;**2. Account details 팝업창**

&#x20;API Credentials 탭의 Username, Password, 및 Signature 값을 아임포트 관리자 콘솔 페이팔 설정 항목에 아래와 같이 맵핑합니다.

* Username = API 사용자 이름
* Password = API 암호&#x20;
* Signature = 서명&#x20;

![API Credentials](<../../../.gitbook/assets/image (22) (1) (1) (1).png>)

<mark style="color:purple;">**구매자 Sandbox 계정 설정**</mark>&#x20;

1. [https://developer.paypal.com/developer/accounts/](https://developer.paypal.com/developer/accounts/) 로그인 > **SANDBOX** > **Accounts** > DEFAULT Personal 계정의 \[**View/edit account**] 클릭

![Accounts 예](<../../../.gitbook/assets/image (24) (1).png>)

**2. Account details 팝업창**&#x20;

Profile 탭의 **Email ID** 및 **Password** 값을 페이팔 결제시 구매자 로그인 계정정보로 사용합니다.

![](<../../../.gitbook/assets/image (21) (1) (1) (1) (1).png>)
{% endtab %}

{% tab title="실 결제" %}
### **실** 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(**일반결제 및 정기결제**) → PG사 페이팔-Express Checkout 선택 → **테스트모드 \[OFF]** → API 사용자 정보 입력 → \[전체 저장] 클릭



![](<../../../.gitbook/assets/image (21) (1) (1) (1).png>)

> **각 항목별 실 운영 정보 값은 페이팔 관리자 페이지에서 아래 절차를 통해 확인합니다.**

1. &#x20;[https://www.paypal.com/](https://www.paypal.com/) 로그인 > 계정 클릭 > 계정 설정 클릭 > "계정 엑세스" 클릭 > "**API 엑세스**"의 업데이트 클릭

![](../../../.gitbook/assets/image.png)

**2) NVP/SOAP API 통합(클래식) 의 API 자격증명 관리 클릭**

\- 참고 : 휴대폰본인인증 절차 필요

![](<../../../.gitbook/assets/image (16) (1) (1) (1) (1).png>)

**3) API 서명보기  "표시" 클릭**

* API 사용자 이름 ****&#x20;
* API 비밀번호
* 서명
{% endtab %}
{% endtabs %}



{% hint style="info" %}
### **참고사항**&#x20;

* Business 계정이 Sandbox이면 구매자 계정도 Sandbox Accounts 목록에 존재하는 Personal 계정으로 결제(사용)해야 합니다.
* Sandbox Accounts 의 Country 가 "US"인 Personal 계정으로 테스트해야 합니다. **판매자와 구매자 계정 국가가 "한국"인 경우 페이팔 정책상 결제가 불가**하며, **판매자는 한국이고 구매자가 미국인 경우는 가능**합니다.
* 판매자와 구매자 계정 국가가 "한국"인 경우 페이팔 정책상 결제가 불가합니다. 판매자와 구매자 중 최소 한사람의 국가가 해외여야 합니다
* 아임포트는 페이팔 정기결제를 지원하지 않습니다.
{% endhint %}

---
description: 대표가맹점과 하위가맹점 설정에 대한 안내 입니다.
---

# 🎈 Agency & Tier 란?

### **하나의 계정으로 하위 가맹점 PG설정이 필요하신 경우(하위가맹점 관리) 아**포트에서 제공하는 **Agent기능**을 이용하시면됩니다.&#x20;

**마스터 계정으로 여러개의 하위가맹점코드(Tier 코드)를 적용하여 등록 하시면 하위 가맹점 별 상점정보 등록 및 결제내역 조회(취소)가 가능합니다.**

(하위가맹점에 대해 3자리 고유코드 부여와 명칭 지정 가능)

{% hint style="info" %}
이용을 원하시면 권한 적용할 차이포트 이메일계정을 아래 이메일 주소로 전달해 주시면 됩니다.&#x20;

[**cs@iamport.kr**](mailto:cs@iamport.kr)****
{% endhint %}

### 자세한 사용방법 안내

아포트 Agent 기능을 통하여 기존보다 더욱 편리하고 효율적으로 가맹점들을 관리할 수 있습니다.

* **Agent 관리자 페이지 체험하기 :** [**admin.iamport.kr**](http://admin.iamport.kr/)
* **테스트용 ID :** [**demo.agency@siot.do**](mailto:demo.agency@siot.do)
* **테스트용 PW : dkdlavhxm (한글로 아임포트)**

데모 버전 Agent 아이디로 하위몰 설정 및 결제내역 조회 기능 체험이 가능합니다.

<주요 기능>

**1. 하위몰별 PG설정**

* 하위 가맹점을 추가 혹은 삭제하고, 하위 가맹점의 PG사 MID 설정 및 관리를 하실 수 있습니다.

![하위 가맹점 PG설정 예시 화면](<../.gitbook/assets/image (13) (1) (1).png>)

![하위 가맹점 PG설정 예시 화면](<../.gitbook/assets/image (24) (1) (1).png>)

![하위 가맹점 코드 생성 화면](<../.gitbook/assets/image (14) (1) (1).png>)

**2. 결제 조회/취소**

* 관리하시는 모든 하위 가맹점의 결제승인 내역을 조회/취소 하실 수 있습니다.

![하위 가맹점 결제내역 조회 예시](<../.gitbook/assets/image (10) (1).png>)

{% hint style="info" %}
**하위 가맹점 결제창 활성화 주의사항**

하위몰별로 결제요청시 **JavaScript SDK** 에서 다음과 같이 **Tier를 구분하여 호출**하실 수 있습니다.

**IMP.agency(가맹점식별코드, Tier(고유)코드 3자리)**

`ex) IMP.agency('imp12345678', '001')`
{% endhint %}

{% hint style="info" %}
**REST API호출시 주의 사항**

REST API호출시에는 Header에 Tier정보를 같이 보내야 해당 Tier에 대한 접근이 가능

HTTP Header 에 아래와 같은 파라미터 설정 필요

`"Tier" : "티어코드 3자리"`
{% endhint %}
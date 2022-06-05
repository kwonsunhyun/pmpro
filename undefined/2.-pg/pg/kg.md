---
description: 이니시스 인증 및 비인증 결제 설정 방법을 안내합니다.
---

# ⌨ KG 이니시스 설정

## 인증**결제**

{% tabs %}
{% tab title="테스트 결제" %}
### 테스트 환경 구성방법

아임포트 관리자페이지( [https://admin.iamport.kr/](https://admin.iamport.kr/) ) > 시스템설정 > PG설정(<mark style="color:red;">**일반결제 및 정기결제**</mark>)에서 PG사 "**KG이니시스(웹표준결제창)**"선택 후 테스트모드\[<mark style="color:red;">**ON**</mark>]상태로 저장하시면 이니시스 일반결제용 테스트상점정보로 자동 설정 됩니다.



> 테스트 모드 설정시 아임포트 테스트 계정으로 결제가 발생됩니다.



![화면예시](<../../../.gitbook/assets/image (15) (1) (1) (1).png>)

{% hint style="info" %}
**KG이니시스 PG상점아이디(MID) : INIpayTest**&#x20;
{% endhint %}
{% endtab %}

{% tab title="실결제" %}
### **실** 환경 구성방법

아임포트 관리자페이지( [https://admin.iamport.kr/](https://admin.iamport.kr/) ) > 시스템설정 > PG설정(<mark style="color:red;">**일반결제 및 정기결제**</mark>)에서 PG사 "**KG이니시스(웹표준결제창)**"선택 후 테스트모드\[<mark style="color:red;">**OFF**</mark>]상태로 변경후 이니시스로 부터 발급받은 MID정보를 기재합니다.

![화면예시](<../../../.gitbook/assets/image (11) (1) (1) (1) (1) (1).png>)
{% endtab %}
{% endtabs %}

## 비 인증 결제

{% hint style="info" %}
KG이니시스 **API방식 빌링키 발급** 은 PG사를 통해 입점가능여부 확인이 우선적으로 필요합니다. 대부분의 경우 '**결제창방식**'으로 지원되며  'API방식'은 PG사 정책으로 인하여 입점이 까다로운 점 참고부탁드립니다.
{% endhint %}

{% tabs %}
{% tab title="결제창 방식" %}
### 테스트 환경 구성방법

아임포트 관리자페이지( [https://admin.iamport.kr/](https://admin.iamport.kr/) ) > 시스템설정 > PG설정(<mark style="color:red;">**일반결제 및 정기결제**</mark>)에서 PG사 "KG이니시스(웹표준결제창)"선택 후 테스트 모드 <mark style="color:red;">**OFF**</mark> 설정 후 빌링결제 테스트용 상점정보를 아래와 같이 설정합니다.

{% hint style="info" %}
**- PG상점아이디(MID) : INIBillTst**\
**- 웹표준결제 signKey : SU5JTElURV9UUklQTEVERVNfS0VZU1RS**\
**- 빌링용 merchantKey : b09LVzhuTGZVaEY1WmJoQnZzdXpRdz09**
{% endhint %}

****

![화면예시](<../../../.gitbook/assets/image (17) (1) (1) (1).png>)

### 실  환경 구성방법

아임포트관리자콘솔( [https://admin.iamport.kr/](https://admin.iamport.kr/) ) > 시스템설정 > PG설정(<mark style="color:red;">**일반결제 및 정기결제**</mark>)에서 PG사 "KG이니시스(웹표준결제창)"선택 후 테스트 모드 <mark style="color:red;">**OFF**</mark> 설정 후 이니시스로 부터 발급받은 **실 계정 정보**를 입력합니다.
{% endtab %}

{% tab title="API 방식" %}
### 테스트 환경 구성방법

아임포트 관리자페이지 [https://admin.iamport.kr/](https://admin.iamport.kr/) > 시스템설정 > PG설정(<mark style="color:red;">**정기결제 및 키인결제**</mark>)에서 PG사 "KG이니시스" 선택 후 **** \[**카드사 심사 전 개발용 계정 설정**] **** 클릭하시면 테스트 상점정보로 자동 세팅 됩니다.&#x20;



![화면예시](<../../../.gitbook/assets/image (25) (1) (1).png>)

### 실  환경 구성방법

* PG상점아이디 : 이니시스에서 이메일로 안내됩니다.
* PG상점 Secret : 계약 당시 별도로 요청하셨다면 1111이 아니라 다른 값으로 발행
{% endtab %}
{% endtabs %}

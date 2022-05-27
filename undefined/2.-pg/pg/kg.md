---
description: 이니시스 인증 및 비인증 결제 설정 방법을 안내합니다.
---

# ⌨ KG 이니시스 설정

## **1.**인증결제

### **KG이니시스-일반 **<mark style="color:red;">**인증결제**</mark>**방식\_테스트모드 설정방법**

아임포트관리자페이지( [https://admin.iamport.kr/](https://admin.iamport.kr/) ) > 시스템설정 > PG설정(<mark style="color:red;">**일반결제 및 정기결제**</mark>)에서 PG사 "KG이니시스(웹표준결제창)"선택 후 테스트모드\[ON]상태로 저장하시면 이니시스 일반결제용 테스트상점정보로 자동 설정 됩니다.

![테스트모드 설정 방법 예시](<../../../.gitbook/assets/image (5).png>)

{% hint style="info" %}
**KG이니시스 PG상점아이디(MID) : INIpayTest**&#x20;
{% endhint %}

### **아임포트 웹훅(Notification URL) 설정방법**

아임포트 Webhook을 사용함으로써 아임포트 서버에 저장된 데이터를 서버에 동기화하고 네트워크 불안정성을 보완할 수 있습니다. - 설정 방법 : 아임포트관리자페이지 > 시스템설정 > 웹훅(Notification) 설정 메뉴에서 "웹훅(Notification) 발송 공통 URL" 항목에 설정

![웹훅 설정 화면 예시](<../../../.gitbook/assets/image (4).png>)

## 2. 비 인증 결제(결제창 방식)

### **KG이니시스-**<mark style="color:red;">**빌링결제**</mark>**(정기결제) 테스트모드 설정방법**

아임포트관리자콘솔( [https://admin.iamport.kr/](https://admin.iamport.kr/) ) > 시스템설정 > PG설정(<mark style="color:red;">**일반결제 및 정기결제**</mark>)에서 PG사 "KG이니시스(웹표준결제창)"선택 후 빌링결제 테스트용 상점정보를 아래와 같이 직접 설정 해 주시기 바랍니다.**.**

* **테스트모드(Sandbox) : OFF**

{% hint style="info" %}
**- PG상점아이디(MID) : INIBillTst**\
**- 웹표준결제 signKey : SU5JTElURV9UUklQTEVERVNfS0VZU1RS**\
**- 빌링용 merchantKey : b09LVzhuTGZVaEY1WmJoQnZzdXpRdz09**
{% endhint %}

![](<../../../.gitbook/assets/image (17).png>)

## **3.** 비 인증 결제(API 방식)

### **PG 상점정보 설정(테스트모드)**

아임포트관리자페이지 [https://admin.iamport.kr/](https://admin.iamport.kr/) > 시스템설정 > PG설정(<mark style="color:red;">**정기결제 및 키인결제**</mark>)에서 PG사 "KG이니시스" 선택 후 **** \[**카드사 심사 전 개발용 계정 설정**] **** 클릭하시면 테스트 상점정보로 자동 세팅 됩니다.&#x20;

![](<../../../.gitbook/assets/image (25).png>)

{% hint style="info" %}
**실운영모드 세팅 방법**&#x20;

* PG상점아이디 : 이니시스에서 이메일로 안내됩니다.
* PG상점 Secret : 계약 당시 별도로 요청하셨다면 1111이 아니라 다른 값으로 발행이 되었을텐데, 별도의 논의가 없었다면 1111로 발행됩니다.
{% endhint %}

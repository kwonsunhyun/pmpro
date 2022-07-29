---
description: 이니시스 인증 및 비인증 결제 설정 방법을 안내합니다.
---

# ⌨ KG 이니시스 설정

## 인증**결제**

{% tabs %}
{% tab title="테스트 결제" %}
### 테스트 환경 구성방법

1. ****[**아임포트 관리자페이지**](https://admin.iamport.kr) > **결제연동** > **테스트 연동 관리** -> **KG이니시스** -> **KG이니시스** -> **추가**
2. **일반결제** 테스트 INIpayTest **설정하기-> 저장**&#x20;



> 테스트 모드 설정시 아임포트 테스트 계정으로 결제가 발생됩니다.



![결제연동 > 테스트 연동 관리 -> KG이니시스 -> KG이니시스 -> 추가](<../../../.gitbook/assets/image (7).png>)

![일반결제 테스트 INIpayTest 설정하기-> 저장](<../../../.gitbook/assets/image (31).png>)

{% hint style="info" %}
**KG이니시스 PG상점아이디(MID) : INIpayTest**&#x20;
{% endhint %}
{% endtab %}

{% tab title="실결제" %}
### **실** 환경 구성방법

1. [**아임포트 관리자페이지**](https://https/admin.iamport.kr)-> **결제연동** -> **실 연동관리 선택**&#x20;
2. **실연동** ->**KG이니시스** -> **KG이니시스**  -> **추가** 선택&#x20;
3. 계약 이후 발급받은 **상점 MID 정보를 기재** 합니다.

![결제연동 -> 실 연동관리 선택](<../../../.gitbook/assets/image (24).png>)

![KG이니시스 -> KG이니시스  -> 추가](<../../../.gitbook/assets/image (15) (1).png>)

![상점 MID 정보를 기재](<../../../.gitbook/assets/image (14) (1).png>)
{% endtab %}
{% endtabs %}

## 비 인증 결제

{% hint style="info" %}
* KG이니시스 **API방식 빌링키 발급** 은 PG사를 통해 입점가능여부 확인이 우선적으로 필요합니다. 대부분의 경우 '**결제창 방식**'으로 지원되며  'API방식'은 PG사 정책으로 인하여 입점이 까다로운 점 참고부탁드립니다.
* **해외카드는 지원되지 않습니다**
{% endhint %}

{% tabs %}
{% tab title="결제창 방식" %}
### 테스트 환경 구성방법

1. [**아임포트 관리자페이지**](https://admin.iamport.kr) > **결제연동** > **테스트 연동 관리** -> **KG이니시스** -> **KG이니시스** -> **추가**
2. **정기결제** 테스트 **`INIBillTst`** **설정하기 -> 저장**&#x20;

****

![결제연동 > 테스트 연동 관리 -> KG이니시스 -> KG이니시스 -> 추가](<../../../.gitbook/assets/image (20) (1).png>)

![정기결제 테스트 INIBillTst 설정하기 -> 저장 ](<../../../.gitbook/assets/image (19).png>)

### 실  환경 구성방법

1. [**아임포트 관리자페이지**](https://https/admin.iamport.kr)-> **결제연동** -> **실 연동관리** 선택 ****&#x20;
2. **KG이니시스** -> **KG이니시스** 선택-> **추가**&#x20;
3. 계약 이후 전달받은 MID 정보를 기재합니다.(**빌링용 MID 기재 필수**)

![아임포트 관리자페이지-> 결제연동 -> 실 연동관리 선택 ](<../../../.gitbook/assets/image (29).png>)

![KG이니시스 -> KG이니시스 선택-> 추가](<../../../.gitbook/assets/image (30) (2).png>)

![계약 이후 전달받은 MID 정보를 기재](<../../../.gitbook/assets/image (32).png>)
{% endtab %}

{% tab title="API 방식" %}
### 테스트 환경 구성방법

[**아임포트 관리자페이지**](https://admin.iamport.kr) -> **결제연동** -> **테스트 연동관리** -> **KG이니시스** 선택 -> <mark style="color:red;">**KG이니시스 API**</mark> -> **추가**&#x20;

![결제연동 -> 테스트 연동관리 -> KG이니시스 선택 -> KG이니시스 API 선택 -> 추가](<../../../.gitbook/assets/image (16).png>)

###

### 실 환경 구성방법

1. [**아임포트 관리자페이지**](https://https/admin.iamport.kr)-> **결제연동** -> **실 연동관리 선택**&#x20;
2. **KG이니시스** 선택 -> <mark style="color:red;">**KG이니시스 API**</mark> -> **추가**&#x20;
3. **계약 이후 전달받은 상점 MID 정보를 기재**&#x20;

![아임포트 관리자페이지-> 결제연동 -> 실 연동관리 선택 ](<../../../.gitbook/assets/image (15) (2).png>)

![KG이니시스 선택 -> KG이니시스 API -> 추가 ](<../../../.gitbook/assets/image (14).png>)

![계약 이후 전달받은 상점 MID 정보 기재](<../../../.gitbook/assets/image (8) (3).png>)
{% endtab %}
{% endtabs %}




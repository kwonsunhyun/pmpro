---
description: JTNET PG사 설정 방법을 확인합니다.
---

# ⌨ JTNET 설정

## 인증결제

{% tabs %}
{% tab title="테스트 결제" %}
### 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(<mark style="color:red;">**일반결제 및 정기결제**</mark>) → PG사 JTNet(tPay) 선택 → 테스트모드 \[ON] → \[전체 저장] 클릭



{% hint style="info" %}
**테스트MID 정보**

* MID : tpaytest0m&#x20;
* Secret 키 : VXFVMIZGqUJx29I/k52vMM8XG4hizkNfiapAkHHFxq0RwFzPit55D3J3sAeFSrLuOnLNVCIsXXkcBfYK1wv8kQ==&#x20;
* 취소비밀번호 : 123456
{% endhint %}



![](<../../../.gitbook/assets/image (20) (1) (1) (1).png>)
{% endtab %}

{% tab title="실 결제" %}
### **실** 환경 구성방법

카드사 심사 완료 후 JTNet에서 발급받은 실상점 정보를 **테스트모드 **<mark style="color:red;">**OFF**</mark> 처리 이후 설정합니다.



![](<../../../.gitbook/assets/image (16) (1) (1) (1) (1).png>)
{% endtab %}
{% endtabs %}

## 비 인증 결제&#x20;

{% tabs %}
{% tab title="결제창 방식" %}
### 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(**일반결제 및 정기결제**) → PG사 JTNet(tPay) 선택 → <mark style="color:red;">**테스트모드 \[OFF]**</mark> → 아래의 상점정보 직접 입력 → \[전체 저장] 클릭



{% hint style="info" %}
**테스트MID 정보**

* PG상점아이디(MID) : tpaytest2m
* PG상점 Secret : coqTx/Taxu9W6dlKPhFuciagoVXr/14ezgoK9+qJCf4bBuo23iRGGWHS4rHIuOSgZ6I/uizX39W/NygDplUYOA==
* 결제취소 비밀번호 : 1234
{% endhint %}



![](<../../../.gitbook/assets/image (24) (1).png>)

### **실** 환경 구성방법

카드사 심사 완료 후 JTNet에서 발급받은 실상점 정보를 **설정합니다.**

****

![](<../../../.gitbook/assets/image (22) (2).png>)
{% endtab %}

{% tab title="API 방식" %}
### 테스트 환경 구성방법(키인결제)

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(<mark style="color:red;">**정기결제 및 키인결제**</mark>) → PG사 JTNet(tPay) 선택 → **카드사 심사 전 개발용 계정 설정** 선택-> \[전체 저장] 클릭



{% hint style="info" %}
**테스트MID 정보(키인결제용도)**

* MID : tpaytest1m &#x20;
* Secret 키 : hgEY70BdDgoJYVOwj5CHsRDQt5a6IieQLQv+Q2rA6nnW+wXP57fH2ZkvUBJW0c9/eF1Rp5QRZ+qjzJ+Knc8r1A==&#x20;
* 취소비밀번호 : 123456
{% endhint %}



![](<../../../.gitbook/assets/image (27) (1).png>)

### 실  환경 구성방법(키인결제)

카드사 심사 완료 후 JTNet 에서 발급받은 실상점 정보를 **** 설정합니다.



![](<../../../.gitbook/assets/image (7) (1).png>)

### 테스트 환경 구성방법(**정기결제**)

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(**정기결제 및 키인결제**) → PG사 JTNet(tPay키인결제) 선택 → 아래의 상점정보 직접 입력 → \[저장] 클릭



{% hint style="info" %}
**테스트MID 정보(정기결)**

* PG상점아이디 : tpaytest2m
* PG상점 Secret : coqTx/Taxu9W6dlKPhFuciagoVXr/14ezgoK9+qJCf4bBuo23iRGGWHS4rHIuOSgZ6I/uizX39W/NygDplUYOA==
* 결제취소비밀번호 : 1234
{% endhint %}



![](<../../../.gitbook/assets/image (12) (2).png>)

### 실  환경 구성방법(정기결제)

카드사 심사 완료 후 JTNet 에서 발급받은 실상점 정보를 **** 설정합니다.



![](<../../../.gitbook/assets/image (6).png>)
{% endtab %}
{% endtabs %}



{% hint style="info" %}
### **체크사항**

JTNet 테스트 모드의 경우 실제 출금 되지만 매일 23:00\~23:50분 사이 자동 취소됩니다.
{% endhint %}

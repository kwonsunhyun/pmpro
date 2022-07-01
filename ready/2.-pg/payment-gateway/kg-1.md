---
description: KG모빌리언스 설정방법을 안내합니다.
---

# ⌨ KG모빌리언스 설정

## 인증결제

{% tabs %}
{% tab title="테스트 결제" %}
### 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/) → 시스템설정 → PG설정(**일반결제 및 정기결제**) → PG사 모빌리언스 선택 → <mark style="color:red;">**테스트모드 \[ON]**</mark> → **서비스 ID** 에 <mark style="color:green;">**170622040674**</mark> 입력 → \[전체 저장] 클릭



![테스트 설정 예시](<../../../.gitbook/assets/image (19) (1).png>)
{% endtab %}

{% tab title="실 결제" %}
### **실** 환경 구성방법

PG사 심사 완료 후 KG모빌리언스에서 발급받은 실상점 정보를 <mark style="color:red;">**테스트모드 OFF**</mark> 이후 설정합니다.



![실 계정 설정 예시](<../../../.gitbook/assets/image (16) (1) (1).png>)
{% endtab %}
{% endtabs %}

## 비 인증 결제

> **KG모빌리언스 비 인증 결제는 휴대폰 결제만 지원합니다.**

{% tabs %}
{% tab title="결제창 방식" %}
### 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(**일반결제 및 정기결제**) → PG사 모빌리언스 선택 → <mark style="color:red;">**테스트모드 \[ON]**</mark> → **서비스 ID** 에 '<mark style="color:green;">**170622040674**</mark>' 입력 → \[전체 저장] 클릭



![테스트 설정 예시](<../../../.gitbook/assets/image (18) (1) (1).png>)
{% endtab %}
{% endtabs %}

{% hint style="success" %}
**KG모빌리언스 테스트 모드의 경우 실제 출금 되지만 매일 23:00\~23:50분 사이 자동 취소됩니다.**
{% endhint %}

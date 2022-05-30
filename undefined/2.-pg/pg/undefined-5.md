---
description: 다날 PG사 설정 방법을 안내합니다.
---

# ⌨ 다날 설정

## 인증**결제**

{% tabs %}
{% tab title="테스트 결제" %}
### 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(<mark style="color:red;">일반결제 및 정기결제</mark>) → PG사 다날-신용카드/계좌이체/가상계좌 선택 → 테스트모드 \[ON] → \[전체 저장] 클릭



![](<../../../.gitbook/assets/image (19).png>)
{% endtab %}

{% tab title="실결제" %}
### **실** 환경 구성방법

카드사 심사 완료 후 다날에서 발급받은 실상점 정보로 설정 해야 합니다.

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(일반결제 및 정기결제) → PG사 **다날-신용카드/계좌이체/가상계좌** 선택 → <mark style="color:red;">**테스트모드 \[OFF]**</mark> →정보입력-> \[전체 저장] 클릭



![](<../../../.gitbook/assets/image (3).png>)
{% endtab %}
{% endtabs %}

## 비 인증 결제

{% tabs %}
{% tab title="결제창 방식" %}
### 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(<mark style="color:red;">일반결제 및 정기결제</mark>) → PG사 **다날-신용카드/계좌이체/가상계좌 선택** → 테스트모드 \[ON] → \[전체 저장] 클릭

![](<../../../.gitbook/assets/image (11).png>)

### 실  환경 구성방법

카드사 심사 완료 후 다날에서 발급받은 실상점 정보로 설정 해야 합니다.

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(일반결제 및 정기결제) → PG사 **다날-신용카드/계좌이체/가상계좌** 선택 → <mark style="color:red;">**테스트모드 \[OFF]**</mark> →정보입력-> \[전체 저장] 클릭

![](<../../../.gitbook/assets/image (14).png>)
{% endtab %}

{% tab title="API 방식" %}
**다날은 API 를 통한 비인증 결제를 지원하지 않습니다.**
{% endtab %}
{% endtabs %}

## 휴대폰 소액결제

{% tabs %}
{% tab title="테스트 환경" %}
### 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(**일반결제 및 정기결제**) → +PG사 추가 → PG사 다날-<mark style="color:red;">**휴대폰소액결제**</mark>**  **  선택 → 테스트모드 \[ON] → \[전체 저장] 클릭

{% hint style="info" %}
**다날 휴대폰결제 테스트용 CPID : A010002002**
{% endhint %}



![](<../../../.gitbook/assets/image (10).png>)
{% endtab %}

{% tab title="실 환경" %}
### 실  환경 구성방법

카드사 심사 완료 후 다날에서 발급받은 실상점 정보로 설정 해야 합니다.

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(**일반결제 및 정기결제**) → +PG사 추가 → PG사 다날-휴대폰소액결제 선택 → <mark style="color:red;">**테스트모드 \[OFF]**</mark> → \[전체 저장] 클릭

![](<../../../.gitbook/assets/image (21).png>)
{% endtab %}
{% endtabs %}


---
description: NHN KCP 설정방법을 안내합니다.
---

# ⌨ NHN KCP 설정

## 인증**결제**

{% tabs %}
{% tab title="테스트결제" %}
### **테스트 환경 구성방법**

1. [아임포트 관리자 콘솔](https://admin.iamport.kr)→ **결제 연동** → **테스트 연동 관리** → PG사 **NHN KCP** 선택 → <mark style="color:red;">**NHN KCP**</mark> ->추가&#x20;
2. **일반결제 테스트 T0000 설정하기** 선택 -> **저장**



> 아임포트 테스트 계정으로 결제가 발생됩니다.



![설정화면 예시](<../../../.gitbook/assets/image (17).png>)

![일반결제 테스트 T0000 설정하기 선택 -> 저장](<../../../.gitbook/assets/image (30).png>)


{% endtab %}

{% tab title="실 결제" %}
### 실 결제 환경 구성방법

KCP 계약 이후 발급받은 **사이트코드**와 **사이트키**를 추가 버튼을 이용하여 올바르게 기입 후 저장합니다.

![설정 예시화면](<../../../.gitbook/assets/image (3) (1) (3).png>) ![정보 입력 화면    ](<../../../.gitbook/assets/image (21).png>)
{% endtab %}
{% endtabs %}

## 비 인증 결제

결제는 일반결제보다 입점이 까다롭기 때문에, KCP를 통하여 입점가능 여부를 먼저 확인해야 합니다.

{% tabs %}
{% tab title="결제창 방식" %}
### 테스트 환경 구성방법

1. [아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 결제 연동 → 테스트 연동 → NHN KCP 선택 → **NHN KCP (정기)** 선택 -> 추가&#x20;
2. 자동으로 설정된 MID값을 화면에서 확인 후 **저장** 버튼을 선택합니다.

![설정 화면 예시](<../../../.gitbook/assets/image (33).png>)

![자동으로 설정된 MID값을 화면에서 확인 후 저장 버튼을 선택](<../../../.gitbook/assets/image (1) (1) (2).png>)

### 실  환경 구성방법

KCP 계약 이후 발급받은 실 사이트코드 정보를 아래와 같은 순서대로 입력합니다.&#x20;

1. **결제연동 -> 실연동 관리 선택**
2. **NHN KCP -> NHN KCP(정기) -> 추가 선택**
3. **사이트코드, 사이트키, 배치결제 그룹 아이디 입력 -> 저장**&#x20;

배치 결제 그룹아이디 입력은 [**링크**](https://www.iamport.kr/download/kcp-billing.pdf)를 클릭하여 자세한 내용을 확인할 수 있습니다.

![결제연동 -> 실연동 관리 선택](<../../../.gitbook/assets/image (28).png>)

![NHN KCP -> NHN KCP(정기) -> 추가 선택](<../../../.gitbook/assets/image (13).png>)

![사이트코드, 사이트키, 배치결제 그룹 아이디 입력 -> 저장](<../../../.gitbook/assets/image (12).png>)
{% endtab %}

{% tab title="API 방식" %}
### 테스트 환경 구성방법

1. [아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 결제 연동 → 테스트 연동 관리 → **NHN KCP** 선택 → **NHN KCP API** 선택->추가
2. 자동으로 설정된 MID정보 확인 후 **저장** 버튼을 선택합니다.

![NHN KCP 선택 → NHN KCP API 선택](<../../../.gitbook/assets/image (22).png>)

![자동으로 설정된 MID정보 확인 후 저장 버튼을 선택합니다.](<../../../.gitbook/assets/image (1) (1).png>)

### 실  환경 구성방법

KCP 계약 이후 발급받은 **사이트코드**와 **사이트키**를 아래 절차대로 기재합니다.

1. **결제 연동 -> 실 연동 관리**
2. **NHN KCP -> NHN KCP API -> 추가**
3. **사이트코드= PG상점 ID/ 사이트키 = PG상점 시크릿 항목에 각각 기재후 배치결제 그룹아이디를 입력**

배치 결제 그룹아이디 입력은 [**링크**](https://www.iamport.kr/download/kcp-billing.pdf)를 클릭하여 자세한 내용을 확인할 수 있습니다.

![결제 연동 -> 실 연동 관리](<../../../.gitbook/assets/image (27).png>)

![NHN KCP -> NHN KCP API -> 추가](<../../../.gitbook/assets/image (7) (1).png>)

![사이트코드= PG상점 ID/ 사이트키 = PG상점 시크릿 항목에 각각 기재후 배치결제 그룹아이디를 입력](<../../../.gitbook/assets/image (18).png>)
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
**비 인증 결제는 인증 결제보다 입점이 까다롭기 때문에 KCP를 통하여 입점가능 여부를 먼저 확인해야 합니다.**
{% endhint %}

{% hint style="info" %}
### 체크사항

* 테스트 모드의 경우 결제시 실제 출금이 이루어지지 않습니다.
* 허브형 카카오페이, 네이버페이는 테스트 모드를 지원하지 않습니다. (KCP와 계약 후 서비스 이용가능
{% endhint %}

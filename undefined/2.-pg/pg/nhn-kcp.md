---
description: NHN KCP 설정방법을 안내합니다.
---

# ⌨ NHN KCP 설정

## 인증**결제 테스트 방법**

### **테스트 결제 환경 구성방법**

[아임포트 관리자 콘솔](https://admin.iamport.kr)→ 시스템설정 → PG설정(일반결제 및 정기결제) → PG사 NHN KCP 선택 → 테스트모드 \[**ON**] → \[<mark style="color:red;">**전체 저장**</mark>] 클릭

![](<../../../.gitbook/assets/image (26).png>)

### 실 결제 환경 구성방법

KCP 계약이후 발급받은 사이트코드와 사이트키를 테스트모드 OFF버튼으로 입력창을 활성화 한후 올바르게 기입후 저장합니다.

![](<../../../.gitbook/assets/image (9) (1) (1).png>)

## 비 인증 결제 테스트 방법

### 결제창 방식

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(일반결제 및 정기결제) → PG사 NHN KCP 빌링결제 선택 → 테스트모드 \[ON] → \[전체 저장] 클릭

![결제창 방식 설정 예시](<../../../.gitbook/assets/image (11) (1).png>)

{% hint style="info" %}
**결제창 방식 실 결제 테스트 방법**

테스트 모드를 <mark style="color:red;">OFF</mark> 처리 한 후 KCP 로 부터 발급받은 MID 정보를 기재합니다.
{% endhint %}

### **REST API 방식**

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(<mark style="color:red;">정기결제 및 키인결제</mark>) → PG사 NHN한국사이버결제 선택 → \[카드사 심사 전 개발용 계정 설정] 클릭 → \[저장] 클릭

![API 방식 설정 예시](<../../../.gitbook/assets/image (24).png>)

> **비 인증 결제 API 방식 실 결제 테스트 방법**
>
> KCP 로 부터 발급받은 MID 정보를 기재합니다.

{% hint style="info" %}
### 체크사항

* 테스트 모드의 경우 결제시 실제 출금이 이루어지지 않습니다.
* 허브형 카카오페이, 네이버페이는 테스트 모드를 지원하지 않습니다. (KCP와 계약 후 서비스 이용가능
{% endhint %}

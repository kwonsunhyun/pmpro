---
description: NHN KCP 설정방법을 안내합니다.
---

# ⌨ NHN KCP 설정

## 인증**결제 테스트 방법**

### **테스트 결제 환경 구성방법**

[아임포트 관리자 콘솔](https://admin.iamport.kr)→ 시스템설정 → PG설정(일반결제 및 정기결제) → PG사 NHN KCP 선택 → 테스트모드 \[**ON**] → \[<mark style="color:red;">**전체 저장**</mark>] 클릭

![NHN KCP 설](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fafa85fe6-e99f-4b44-9b0c-fd2c0bee0a17%2FUntitled.png\&blockId=b3792ff9-ce01-4991-8008-1b7abbafa47b)

### 실 결제 환경 구성방법

KCP 계약이후 발급받은 사이트코드와 사이트키를 테스트모드 OFF버튼으로 입력창을 활성화 한후 올바르게 기입후 저장합니다.

![](<../../../.gitbook/assets/image (9) (1) (1).png>)

## 비 인증 결제 테스트 방법

### 결제창 방식

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(일반결제 및 정기결제) → PG사 NHN KCP 빌링결제 선택 → 테스트모드 \[ON] → \[전체 저장] 클릭

![결제창 방식 설정 예시](<../../../.gitbook/assets/image (11).png>)

### **REST API 방식**

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(<mark style="color:red;">정기결제 및 키인결제</mark>) → PG사 NHN한국사이버결제 선택 → \[카드사 심사 전 개발용 계정 설정] 클릭 → \[저장] 클릭

![API 방식 설정 예시](<../../../.gitbook/assets/image (24).png>)

{% hint style="info" %}
### 체크사항

* 테스트 모드의 경우 결제시 실제 출금이 이루어지지 않습니다.
* 허브형 카카오페이, 네이버페이는 테스트 모드를 지원하지 않습니다. (KCP와 계약 후 서비스 이용가능
{% endhint %}

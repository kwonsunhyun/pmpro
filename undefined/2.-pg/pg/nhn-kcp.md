---
description: NHN KCP 설정방법을 안내합니다.
---

# ⌨ NHN KCP 설정

### 체크사항

1. KCP 테스트 모드의 경우 결제시 실제 출금이 이루어지지 않습니다.

2\. KCP의 허브형인 카카오페이, 네이버페이는 테스트 모드를 지원하지 않습니다. (KCP와 계약 후 서비스 이용가능)

### 설정 방법

#### 1. 아임포트 관리자콘솔에서 회원가입

[https://admin.iamport.kr](https://admin.iamport.kr) 이메일 계정으로 회원가입 진행

#### 2. 테스트 모드 설정

> 카드사 심사 완료 후에는 KCP에서 발급받은 실상점 정보로 설정 해야 합니다.

### **일반결제(인증) 테스트 방법**

[아임포트 관리자 콘솔](https://admin.iamport.kr)→ 시스템설정 → PG설정(일반결제 및 정기결제) → PG사 NHN KCP 선택 → 테스트모드 \[**ON**] → \[<mark style="color:red;">**전체 저장**</mark>] 클릭

![NHN KCP 설](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fafa85fe6-e99f-4b44-9b0c-fd2c0bee0a17%2FUntitled.png\&blockId=b3792ff9-ce01-4991-8008-1b7abbafa47b)

### 실 결제 테스트 방법

KCP 계약이후 발급받은 사이트코드와 사이트키를 테스트모드 OFF버튼으로 입력창을 활성화 한후 올바르게 기입후 저장합니다.

![](<../../../.gitbook/assets/image (9) (1) (1).png>)

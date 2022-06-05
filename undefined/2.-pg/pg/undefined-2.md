---
description: 다우 설정 방법을 안내합니다.
---

# ⌨ 다우 설정

## 인증**결제**

{% tabs %}
{% tab title="테스트 결제" %}
### 테스트 환경 구성방법



### \[아임포트 관리자 콘솔 설정 사항]

1. [아임포트 관리자 콘솔](https://admin.iamport.kr/) 로그인
2. 상단 **시스템설정** 메뉴 선택&#x20;
3. **PG설정**(**일반결제 및 정기결제**)메뉴  선택&#x20;
4. 왼쪽 **PG사 추가** 선택&#x20;
5. **페이조아(다우데이터) 선택**&#x20;
6. 테스트모드 \[<mark style="color:red;">**ON**</mark>] 선택&#x20;
7. **전체저장**



![테스트 설정 예시](<../../../.gitbook/assets/image (2).png>)



{% hint style="info" %}
### **확인사항**

* 다우 데이타는 PG가입신청 이후 가맹점별 테스트용 상점정보(KEY)가 발급됩니다.
* 상점아이디 발급 시 판매상품 유형(실물 / 디지털)을 확인하시고 발급요청 해야 합니다.
* 결제연동키는 결제 취소시 필요한 키 값을 의미합니다.
{% endhint %}

###

### \[페이조 관리자 콘솔 설정 사항]

각 결제수단별 정상적인 결제 결과를 수신하기 위한 아래 설정이 반드시 필요합니다.

1. [페이조아 관리자페이지](https://agent.kiwoompay.co.kr/) 로그인
2. 상단 **고객지원** > **연동정보설정** 메뉴 클릭

![페이 조아 메뉴 위치](<../../../.gitbook/assets/image (29).png>)



&#x20;3\. 연동 정보 설정 화면에서 하단 **CPID**를 선택 후 **조회하기** 버튼 선택

![연동정보 설정](<../../../.gitbook/assets/image (26).png>)

4\. 계약된 결제수단 별로 하단의 **결과통지 URL 설정**

> [https://service.iamport.kr/daou\_payments/result](https://service.iamport.kr/daou\_payments/result)

![결과통지 URL 설정](<../../../.gitbook/assets/image (20).png>)
{% endtab %}

{% tab title="실 결제" %}
**테스트 설정과 동일하며 실 결제를 위해서는 **<mark style="color:red;">**테스트모드 \[OFF]**</mark>** 설정만 진행합니다.**
{% endtab %}
{% endtabs %}


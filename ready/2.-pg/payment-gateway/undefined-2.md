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

각 결제수단별 **정상적인 결제 결과를 수신**하기 위한 아래 설정이 반드시 필요합니다.

1. [페이조아 관리자페이지](https://agent.kiwoompay.co.kr/) 로그인
2. 상단 **고객지원** > **연동정보설정** 메뉴 클릭

![페이 조아 메뉴 위치](<../../../.gitbook/assets/image (29) (1).png>)



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

## 비 인증 결제

{% tabs %}
{% tab title="API 방식" %}
### 정기결제 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(**정기결제 및 키인결제**) → PG사 페이조아(다우데이타) 선택 → 아래 정기결제용 상점정보 입력 → \[저장] 클릭



> * 정기결제용 상점아이디(CPID) : **CTS17266**&#x20;
> * 정기결제용 Secret 키 : **831a32f930a2ee38175bb461ff2113dea80d161e23fc00e05ee5b81fd4322534**

****

![테스트 설정 예시](<../../../.gitbook/assets/image (10) (1).png>)

###

### 키인결제(1회성 결제) 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(**정기결제 및 키인결제**) → PG사 페이조아(다우데이타) 선택 → \[<mark style="color:red;">**카드사 심사 전 개발용 계정 설정**</mark>] 클릭 → \[저장] 클릭&#x20;



> <mark style="color:red;">**카드사 심사 전 개발용 계정 설정**</mark>** 버튼 선택시** 아래 정보가 자동 기입됩니다.
>
> * 키인결제용 상점아이디(CPID) : **CTS16629**&#x20;
> * 키인결제용 Secret 키 : **7f59ab6239259b191e2806111734c17c4650301ae0f241d2939c747176b4f6aa**

****

![테스트 설정 예시](<../../../.gitbook/assets/image (5) (1).png>)

{% hint style="info" %}
### **키인 결제 필수 파라미터 변경 테스트 방법**

CPID 값에 따라 키인 결제시 필수 파라미터를 변경하여 테스트 할수 있습니다.

* **카드번호 + 비밀번호 + 유효기간 + 생년월일**

&#x20;    \- CPID : CTS16629

&#x20;    \- Secret : 7f59ab6239259b191e2806111734c17c4650301ae0f241d2939c747176b4f6aa

* **카드번호 + 유효기간**

&#x20;    \- CPID :  CTS16628

&#x20;    \- Secret : 9e810e78e4d8ac765f8f04f1f3132da0c4891a2c04f6ee5a142bc333070b68a9
{% endhint %}



{% hint style="success" %}
### **확인사항**

* 페이조아의 정기결제는 REST API 방식만 지원합니다.
* 페이조아 테스트 모드의 경우 실제 출금 되지만 매일 23:00\~23:50분 사이 자동 취소됩니다.
* **키인결제**(일회성결제)와 **정기결제용** 테스트 상점아이디가 상이하오니 유의하여 연동해주세요!
* 상점아이디 발급 시 판매상품 유형(실물 / 디지털)에 맞게 발급 받아 주세요.
{% endhint %}
{% endtab %}

{% tab title="결제창 방식" %}
**결제창 방식 정기 결제는 지원하지 않습니다.**
{% endtab %}
{% endtabs %}
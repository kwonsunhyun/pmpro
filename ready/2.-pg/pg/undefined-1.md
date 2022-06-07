---
description: 토스 간편결제 설정 방법을 안내합니다.
---

# ⌨ 토스간편결제 설정

## 일반**결제**

{% tabs %}
{% tab title="테스트 결제" %}
### 테스트 환경 구성방법

[아임포트 관리자 콘솔](https://admin.iamport.kr/)→ 시스템설정 → PG설정(**일반결제 및 정기결제**) → PG사 \[간편결제]토스 선택 → <mark style="color:red;">**테스트모드 \[ON]**</mark> → 테스트 apikey 입력 > \[전체 저장] 클릭



> * 테스트 상점아이디 : **tosstest**&#x20;
> * 테스트 apiKey : **sk\_test\_w5lNQylNqa5lNQe013Nq**



![테스트 설정 예시](<../../../.gitbook/assets/image (3).png>)
{% endtab %}

{% tab title="실 결제" %}
### **실** 환경 구성방법

**테스트모드 **<mark style="color:red;">**OFF**</mark> 처리 이후 카드사 심사 완료 후 토스페이에서 발급받은 실상점 정보로 설정 해야 합니다.



![실 환경 정보 설정 예시](<../../../.gitbook/assets/image (22).png>)
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
**아임포트는 토스 간편결제 정기결제를 지원하지 않습니다.**
{% endhint %}

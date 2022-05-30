---
description: 결제요청의 주체를 가맹점 서버로 가져갈수 있는 서비스 입니다.
---

# 🔏 Confirm Process

### 해당 서비스는 결제요청직전에 가맹점 측에 결제의사를 최종적으로 확인하는 서비스입니다.

![](<../.gitbook/assets/image (16) (1).png>)

![Confirm Process](<../.gitbook/assets/image (3).png>)

{% hint style="info" %}
**해당 서비스가 반드시 필요한 가맹점은 아래와 같은 경우입니다.**&#x20;

* 판매 제품이 재고적으로 소량인 경우
* 선착순방식으로 결제가 진행되는 경우
* 결제 요청전 마지막으로 가맹점에서 처리하고 싶은 업무처리가 있는 경우&#x20;
{% endhint %}

![Confirm Process](<../.gitbook/assets/image (14) (1).png>)

### **판매 제품이 재고적으로 소량인 경우**

가맹점 판매 제품이 명품 또는 매우 인기가 높은 품목인 경우 결제 시 동시 접속자로 인해 경쟁이 치열해지는 경우 결제 직전 가맹점서버에서 재고수량을 한번더 확인하고 수량이 있는 경우에만 결제가 요청되도록 처리 할 수 있습니다. 만약 Confirm Process를 설정하지 않는 경우 결제는 되었지만 재고가 없어서 제품 발송을 약속된 일자에 처리하지 못하거나 혹은 이로인해 취소처리가 발생하여 고객 결제 만족 경험도를 떨어트리는 상황이 발생됩니다.

![](<../.gitbook/assets/image (14).png>)

### **선착순 방식으로 결제가 진행되는 경우**

마라톤 참가 신청, 인기 콘서트 티켓팅, OO Day 와 같은 특별 할인행사 처럼 특정 시간에 결제가 활성화되는 결제방식을채택하고 있는 가맹점인 경우 특정시간에 매우 많은 고객이 동시에 결제 요청이 유입되며 이에따라 결제 요청 직전에 가맹점 서버에서 재고수량 파악이 필요합니다.

![](<../.gitbook/assets/image (4) (1).png>)

### **결제 직전 가맹점에서 업무로직을 한번 더 수행하고 싶은 경우**

이밖에 다른 사유로 가맹점 측에서 결제 직전 자체업무 처리가 필요한 경우(결제 직전 가맹점 서버 헬스체크 등) 해당 서비스를 이용합니다.

![](<../.gitbook/assets/image (5) (1) (1).png>)

{% hint style="info" %}
**Confirm Process 신청 방법**

기술지원 메일([support@iamport.kr](mailto:support@iamport.kr))로 <mark style="color:red;">**가맹점식별코드**</mark>를 기재하여 메일 발송
{% endhint %}

![가맹점 식별코드 확인방법](<../.gitbook/assets/image (18) (1) (1) (1).png>)

### **Confirm Process 이용방법**

Confirm Process 이용시 가맹점은 Javascript request\_pay() 함수 호출시 **confirm\_url** 파라미터를 정의하고 해당 파라미터의 가맹점 EndPoint URL을 설정합니다.

{% code title="JavaScript SDK" %}
```jsx
... 
confirm_url : ‘가맹점 EndPoint URL기재’,
...
```
{% endcode %}

해당 URL이 설정되면 당사에서 결제 요청 직전 해당 URL 로 **HTTP 통신**이 진행되며 (HTTP body상에 웹훅과 동일한 Data가 내려갑니다.)

> `imp_uid`: 결제번호
>
> `merchant_uid`: 주문번호
>
> `status`: 결제 결과

해당 요청에 대한 가맹점 응답으로 HTTP Status **200** 응답을 주시는 경우 결제를 요청합니다.

(<mark style="color:red;">**200응답이 아닌 경우 결제가 진행되지 않습니다**</mark>.(**`실패처리`**)

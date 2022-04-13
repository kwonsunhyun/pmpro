---
description: customer_uid 로 정기(예약)결제 구현방법을 안내합니다.
---

# 🪧 빌링키를 이용한 정기결제

#### [빌링키 발급](../../api/rest-api-access-token/api/api-1-1.md) 또는 [비 인증 결제(일회성)](../../api/rest-api-access-token/api/api-1.md) API를 이용하여 customer\_uid 를 획득했다면 원하는 형태의 정기 또는 예약결제를 이용할 수 있습니다.

### <mark style="color:blue;">**STEP 01.**</mark> 결제 예약하기

미래 특정 시점에 결제가 진행되도록 결제를 예약할 수 있습니다. 차이포트 <mark style="color:blue;">**결제 예약 API**</mark>를 이용하여 원하시는 시점에 결제 예약을 손쉽게 등록 할 수 있습니다.&#x20;

{% tabs %}
{% tab title="server-side" %}
{% code title="Node.js" %}
```javascript
// 결제 예약
  axios({
    url: \`https://api.iamport.kr/subscribe/payments/schedule\`,
    method: "post",
    headers: { "Authorization": access_token }, 
    data: {
      customer_uid: "gildong_0001_1234", // 카드(빌링키)와 1:1로 대응하는 값
      schedules: [
        {
          merchant_uid: "order_monthly_0001", // 주문 번호
          schedule_at: 1519862400, // 결제 시도 시각 in Unix Time Stamp. 예: 다음 달 1일
          amount: 8900,
          name: "월간 이용권 정기결제",
          buyer_name: "홍길동",
          buyer_tel: "01012345678",
          buyer_email: "gildong@gmail.com"
        }
      ]
    }
  });
```
{% endcode %}
{% endtab %}
{% endtabs %}

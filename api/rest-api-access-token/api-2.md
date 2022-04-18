---
description: 모든 결제내역을 취소할 수 있는 API 를 안내합니다.
---

# ❌ 결제취소 API

### **결제수단 및 PG사와 상관없이 취소 및 부분취소가 가능합니다.**

{% swagger method="post" path="/payments/cancel" baseUrl="https://api.iamport.kr" summary="승인된 결제를 취소합니다." %}
{% swagger-description %}
신용카드/실시간계좌이체/휴대폰 소액결제의 경우 즉시 취소처리가 이뤄지게 되며 가상계좌의 경우는 환불받으실 계좌정보를 같이 전달해주시면 환불정보가 PG사에 등록되어 익영업일에 처리됩니다.

**(가상계좌 환불관련 특약계약 필요)**
{% endswagger-description %}

{% swagger-parameter in="body" name="imp_uid" type="String" required="true" %}
<mark style="color:red;">

**차이포트 거래고유번호**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="merchant_uid" type="String" %}
**주문번호 (imp_uid 누락시 필수)**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="Double" required="true" %}
<mark style="color:red;">

**취소 요청금액**

</mark>

** (누락시 전액취소)**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tax_free" type="Double" %}
취소요청금액 중 면세금액 (누락되면 0원처리)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="checksum" type="Double" %}
현재시점의 취소 가능한 잔액.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="reason" type="String" %}
취소사유
{% endswagger-parameter %}

{% swagger-parameter in="body" name="refund_holder" type="String" %}
환불계좌 예금주 (

**가상계좌**

 취소시 필수)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="refund_bank" type="String" %}
환불계좌 은행코드 (하단 은행코드표 참조, 

**가상계좌 취소시**

 필수)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="refund_account" type="String" %}
환불계좌 계좌번호 (

**가상계좌**

 취소시 필수)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="refund_tel" type="String" %}
환불계좌 예금주 연락처(

**가상계좌**

 취소,

<mark style="color:red;">

**스마트로 PG사 인경우 필수**

</mark>

 )
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="취소 성공" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="인증 Token이 전달되지 않았거나 유효하지 않은 경우" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

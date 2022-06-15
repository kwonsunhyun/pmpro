---
description: 페이코 주문상품의 상태를 변경합니다
---

# ⌨ 주문상태 단건 수정 API

### 판매상품의 주문상태를 변경합니다.

{% swagger method="post" path="/payco/orders/status/{imp_uid}" baseUrl="https://api.iamport.kr" summary="페이코 주문상품 단건상태 변경" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="imp_uid" type="String" required="true" %}
<mark style="color:red;">

**아임포트 고유번호**

</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="status" type="String" required="true" %}
<mark style="color:red;">**주문상태코드**</mark>

`DELIVERY_START (배송시작-출고지시)`

`PURCHASE_DECISION (구매확정)`

`CANCELED (취소)`
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
{% tabs %}
{% tab title="PaycoStatusResponse" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**`response` **<mark style="color:red;">**(PaycoStatusAnnotation, optional)**</mark>
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="PaycoStatusAnnotation" %}
**`status`**<mark style="color:red;">**`*`**</mark><mark style="color:green;">**`string`**</mark>

**`PAYCO 주문변경된 상태`**

&#x20;\['DELIVERY\_START', 'PURCHASE\_DECISION', 'CANCELED']
{% endtab %}
{% endtabs %}
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="인증 Token이 전달되지 않았거나 유효하지 않은 경우" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

<details>

<summary>Response Model Schema</summary>

```
{
  "code": 0,
  "message": "string",
  "response": {
    "status": "DELIVERY_START"
  }
}
```

</details>

{% hint style="success" %}
**Swagger Test Link**

****[**https://api.iamport.kr/#!/payco/changeOrderStatus**](https://api.iamport.kr/#!/payco/changeOrderStatus)****
{% endhint %}

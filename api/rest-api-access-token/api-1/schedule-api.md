---
description: 원하는 시점에 결제를 예약하고 결제 결과를 Webhook으로 받을 수 있는 API입니다.
---

# ⌨ 결제 예약(Schedule) API

#### customer\_uid 를 이용하여 비 인증 결제 요청을 예약할수 있는 API 입니다. 결제 요청에 대한 결과는 **notice\_url** 에 설정한 EndPoint URL 로 웹훅을 통해 결제 결과를 수신(POST request)받을 수 있습니다.

{% swagger method="post" path="/subscribe/payments/schedule" baseUrl="https://api.iamport.kr" summary="결제 예약(Schedule) API" %}
{% swagger-description %}
customer_uid와 연결된 빌링키로 결제가 예약됩니다. 기존에 발급한 customer_uid 를 이용하지 않고 새로운 값을 지정하는 경우 카드정보를 반드시 기재하여야 하며 요청이 성공적으로 처리되면 빌링키 발급과 결제예약이 동시에 이루어 집니다.
{% endswagger-description %}

{% swagger-parameter in="body" name="customer_uid" type="String" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" %}

{% endswagger-parameter %}
{% endswagger %}

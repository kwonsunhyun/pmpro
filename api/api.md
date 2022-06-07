---
description: 아임포트 API 를 소개합니다.
---

# 📋 아임포트 API 소개

### 아임포트 API를 이용하기 위한 HTTP Header 설정을 안내합니다.

1. [**/users/getToken**](rest-api-access-token.md) 에서 **API Key** & **API secret**을 사용해 <mark style="color:red;">**`access_token`**</mark>을 발급받습니다.
2. API 호출 시 <mark style="color:red;">**`access_token`**</mark>을 **`Authorization:`**<mark style="color:red;">**`access_token`**</mark> 또는 **`X-ImpTokenHeader:`**<mark style="color:red;">**`access_token`**</mark>으로 HTTP header를 통해 전달합니다.

{% hint style="info" %}
**Content-Type**

아포트가 제공하는 모든 API Content-Type은 아래와 같습니다.

**Application.json;charset=UTF-8**
{% endhint %}

{% hint style="warning" %}
**Agency 가맹점**&#x20;

아포트 API 호출시 **`HTTP Header`** 에 아래 파라미터 설정이 필요합니다. 하위 가맹점(Tier)은 **Agent 계정의** <mark style="color:blue;">**`API key`**</mark> 와 <mark style="color:blue;">**`Secret`**</mark> 을 사용해야 합니다.

* **`"Tier" : "`**<mark style="color:red;">**`Tier code`**</mark>(하위 가맹점 Tier Code)"
{% endhint %}

### API 명세 확인방법

아임포트 API 응답부 명세를 자세히 확인 하기 위해서는 아래와 같이 **Response** 항목 **HTTP Status **<mark style="color:green;">**200**</mark> 항목 선택시 자세한 출력 명세를 확인할 수 있습니다.

![응답항목 예시](<../.gitbook/assets/image (18) (1) (1) (1) (1).png>)

{% hint style="info" %}
**API Swagger 사이트**

아임포트는 Swagger API 명세를 지원합니다.

****[**https://api.iamport.kr**](https://https/api.iamport.kr)****
{% endhint %}

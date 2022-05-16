---
description: 차이포트 API 를 소개합니다.
---

# 📋 차이포트 API 소개

### 차이포트 API를 이용하기 위한 HTTP Header 설정을 안내합니다.

1. [**/users/getToken**](rest-api-access-token.md) 에서 **API Key** & **API secret**을 사용해 <mark style="color:red;">**`access_token`**</mark>을 발급받습니다.
2. API 호출 시 <mark style="color:red;">**`access_token`**</mark>을 **`Authorization:`**<mark style="color:red;">**`access_token`**</mark> 또는 **`X-ImpTokenHeader:`**<mark style="color:red;">**`access_token`**</mark>으로 HTTP header를 통해 전달합니다.

{% hint style="info" %}
**Content-Type**

차이포트가 제공하는 모든 API Content-Type은 아래와 같습니다.

**Application.json;charset=UTF-8**
{% endhint %}

{% hint style="warning" %}
**Agency 가맹점**&#x20;

차이포트 API 호출시 **`HTTP Header`** 에 아래 파라미터 설정이 필요합니다. 하위 가맹점(Tier)은 **Agent 계정의** <mark style="color:blue;">**`API key`**</mark> 와 <mark style="color:blue;">**`Secret`**</mark> 을 사용해야 합니다.

* **`"Tier" : "`**<mark style="color:red;">**`Tier code`**</mark>(하위 가맹점 Tier Code)"
{% endhint %}

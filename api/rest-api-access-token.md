---
description: Access Token 을 발급하는 방법을 설명합니다.
---

# 🖇 REST API Access Token

### 아임포트의 모든 REST API 이용을 위해서는 토큰 발급 및 설정이 필수입니다.

결제 정보와 같은 사적 리소스(private resource)에 대한 접근 권한을 얻으려면 가맹점은 access token을 발급 받아서 차이 포트 REST API 요청에 포함해야 합니다.

### 토큰 발급받기 <a href="#undefined" id="undefined"></a>

{% hint style="danger" %}
**서버 사이드에서 토큰 발급하기**

Access token 발급 요청을 **클라이언트 사이드에서 하면 요청 시 필요한 **<mark style="color:red;">**`REST API`**</mark>**` ``키`와 **<mark style="color:red;">**`REST API Secret`**</mark>**이 노출되어 보안상 안전하지 않기 때문에** 토큰 발급 요청은 **반드시 서버 사이드에서 해야합니다.**
{% endhint %}

### <mark style="color:blue;">**STEP 01.**</mark>  발급 요청하기

관리자 콘솔에서 확인한 **`REST API 키`**와 **`REST API Secret`**로 REST API([POST https://api.iamport.kr/users/getToken](https://api.iamport.kr/#!/authenticate/getToken))를 호출하여 access token 발급을 요청하는 예제입니다.

![관리자 콘솔 REST API키 & REST API Secret](<../.gitbook/assets/image (18) (1) (1) (1) (1).png>)

{% tabs %}
{% tab title="curl" %}
{% code title="server-side" %}
```url
curl -H "Content-Type: application/json" POST -d '{"imp_key": "REST API키", "imp_secret":"REST API Secret"}' https://api.iamport.kr/users/getToken
```
{% endcode %}
{% endtab %}

{% tab title="Node.js" %}
{% code title="server-side" %}
```javascript
// 인증 토큰 발급 받기
  axios({
    url: "https://api.iamport.kr/users/getToken",
    // POST method
    method: "post", 
    // "Content-Type": "application/json"
    headers: { "Content-Type": "application/json" }, 
    data: {
      // REST API키
      imp_key: "imp_apikey", 
      // REST API Secret
      imp_secret: "ekKoeW8RyKuT0zgaZsUtXXTLQ4AhPFW3ZGseDA6bkA5lamv9OqDMnxyeB9wqOsuO9W3Mx9YSJ4dTqJ3f" 
    }
  });
```
{% endcode %}
{% endtab %}
{% endtabs %}

### <mark style="color:blue;">**STEP 02.**</mark>  Access Token 받기

발급 요청에 대한 응답으로 access token 을 받을 수 있습니다.

{% code title="Response" %}
```json
{
    "code": 0,
    "message": null,
    "response":{
      "access_token": "a9ace025c90c0da2161075da6ddd3492a2fca776", // access token
      "now": 1512446940, // 아임포트 REST API 서버의 현재 시간
      "expired_at": 1512448740, // token의 만료 시간 (UNIX timestamp, KST 기준)
    },
  }
```
{% endcode %}

{% hint style="info" %}
**기준 NTP서버**

아임포트 REST API 서버는 <mark style="color:red;">**Google Public NTP**</mark> 를 이용하여 기준시간과 동기화하고 있습니다.
{% endhint %}

### <mark style="color:blue;">**STEP 03.**</mark>  토큰 사용하기

발급받은 access token을 사용하여 아임포트 REST API 요청을 할 수 있습니다. 아임포트 REST API는 **Bearer** 인증 방식을 사용하기 때문에 HTTP 요청 헤더에 access token을 다음과 같은 형식으로 포함합니다.

> Authorization: **Bearer** a9ace025c90c0da2161075da6ddd3492a2fca776

{% tabs %}
{% tab title="curl" %}
Access token을 **헤더에 포함**하여 결제 상세 내역 조회 API 를 요청을 하는 예제입니다

{% code title="server-side" %}
```
curl -H "Content-Type: application/json" -H "Authorization: Bearer a9ace025c90c0da2161075da6ddd3492a2fca776" https://api.iamport.kr/payments/imp_448280090638
```
{% endcode %}
{% endtab %}

{% tab title="Node.js" %}
{% code title="server-side" %}
```json
axios({
    url: "https://api.iamport.kr/payments/imp_448280090638",
    method: "get", // GET method
    headers: {
      // "Content-Type": "application/json"
      "Content-Type": "application/json", 
      // 발행된 액세스 토큰
      "Authorization": "Bearer a9ace025c90c0da2161075da6ddd3492a2fca776" 
    }
  });
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Access Token의 재발행과 재사용 <a href="#access-token" id="access-token"></a>

Access token의 만료기한은 발행 시간부터 **30분**입니다. 토큰은 **만료기한이 지나면 사용할 수 없습니다**. 만료된 토큰으로 API 요청을 하면 <mark style="color:red;">**`401 Unauthorized`**</mark>`응답을 받습니다.`

> * 재발행 (만료 후 발급): 새로운 access token을 발급한다. (만료기한: 발행시간 후 30분)
> * 재사용 (만료 전 발급): 기존 access token을 발급한다. (만료기한: 기존과 동일, 단 기존 만료시간 전 1분이내 요청 시 5분 연장 됨)

![](../.gitbook/assets/2.svg)

{% hint style="info" %}
**만료기한 5분 연장**

Access token의 재사용과 만료기한 5분 연장 동작방식은 다음과 같은 상황을 고려해서 설계되었습니다.

* 한 가맹점에서 여러 대의 웹서버가 동시에 경쟁적으로 REST API(`/users/getToken`)를 호출하는 상황
* 한 가맹점에서 여러 대의 웹서버가 시간 동기화 되어있지 않은 상황
{% endhint %}

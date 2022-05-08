---
description: 본인인증 결과를 조회합니다.
---

# ⌨ 본인인증 결과조회 API

### 본인인증된 결과를 조회할 때 사용합니다.

{% swagger method="get" path="/certifications/{imp_uid}" baseUrl="https://api.iamport.kr" summary="본인인증 결과를 imp_uid를 이용하여 조회합니다." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" required="true" name="imp_uid" type="String" %}
<mark style="color:red;">

**차이포트 인증고유번호**

</mark>
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="조회성공" %}
{% tabs %}
{% tab title="CertificationResponse" %}
**`code`  **<mark style="color:red;">**\***</mark>** **<mark style="color:purple;">**integer**</mark>

**응답코드**

0이면 정상적인 조회, 0 이 아닌 값이면 message를 확인해봐야 합니다



**`message`  **<mark style="color:red;">**\***</mark>** **<mark style="color:green;">**string**</mark>

**응답메세지**

code 값이 0이 아닐 때, '존재하지 않는 결제정보입니다'와 같은 오류 메세지를 포함합니다



**response** <mark style="color:red;">**(CertificationAnnotation, optional)**</mark>
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="CertificationAnnotation" %}
**`imp_uid`**  <mark style="color:red;">\*</mark> <mark style="color:green;">**string**</mark>&#x20;

**`인증고유번호`**

****

**`merchant_uid`    **<mark style="color:green;">**string**</mark>

**`주문번호`**

****

**`pg_tid`  **<mark style="color:blue;">****</mark>**  **<mark style="color:green;">**string**</mark>

**`PG사 인증결과 고유번호` **&#x20;

****

**`pg_provider`** <mark style="color:red;">**\***</mark>**  **<mark style="color:green;">**string**</mark>&#x20;

**`본인인증 제공 PG사 명칭`**



**`name`      **<mark style="color:green;">**string**</mark>** **&#x20;

**`실명` **&#x20;

&#x20;

**`gender`**  <mark style="color:green;">**string**</mark>

**`성별` **<mark style="color:green;">****</mark>&#x20;

* male:남성
* female:여성



**`birthday`   **<mark style="color:green;">**string**</mark>

**`생년월일` **<mark style="color:green;">****</mark>&#x20;

ISO8601 형식의 문자열. <mark style="color:red;">YYYY-MM-DD</mark> 10자리 문자열



**`foreigner`  **<mark style="color:green;">****</mark>**  **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">****</mark>**  **<mark style="color:orange;">**boolean**</mark>

**`외국인여부`**

<mark style="color:red;">다날 본인인증서비스 계약시</mark> 외국인 구분기능 추가 요청을 해주셔야 사용이 가능합니다

* true <mark style="color:orange;">****</mark> : 외국인
* false : 내국인

<mark style="color:green;">****</mark>

&#x20;**`phone`    **<mark style="color:green;">**string**</mark>

**`휴대폰번호` **<mark style="color:green;">****</mark>&#x20;

특수기호없이 숫자로만 구성된 휴대폰번호가 전달. 통신사 사전승인이 이뤄지지 않으면 phone 속성은 존재하지 않습니다. 통신사 사전승인이 필요하므로 **cs@iamport.kr **<mark style="color:green;">****</mark> 로 다날 CPID 와 함께 사용승인 요청이 필요합니다.&#x20;



**`carrier`**  <mark style="color:green;">**string**</mark>

**`휴대폰번호의 통신사` **<mark style="color:green;">****</mark>&#x20;

통신사 사전승인이 필요하므로 **cs@iamport.kr **<mark style="color:green;">****</mark> 로 다날 CPID 와 함께 사용승인 요청이 필요합니다.&#x20;

* SKT
* KT
* LGT
* SKT\_MVNO
* KT\_MVNO
* LGT\_MVNO



**`certified`   **<mark style="color:green;">****</mark>**   **<mark style="color:red;">**\***</mark>**  **<mark style="color:green;">****</mark>**  **<mark style="color:orange;">**boolean**</mark>

**`인증성공여부`**

&#x20;****&#x20;

**`certified_at`**  <mark style="color:red;">****</mark>**  **<mark style="color:green;">**string**</mark>

**`인증처리시각` ** (UNIX timestamp) <mark style="color:green;">****</mark>&#x20;

<mark style="color:green;">****</mark>

**`unique_key`  **<mark style="color:green;">**string**</mark>

**개인 고유구분 식별키 **<mark style="color:green;">****</mark>** (`CI`)**

****

**`unique_in_site` **<mark style="color:green;">****</mark>**     **<mark style="color:green;">**string**</mark>

**가맹점 내 개인 고유구분 식별키 (`DI`)**

****

**`origin`    **<mark style="color:green;">**string**</mark>

**본인인증 프로세스가 진행된 웹 페이지의 `URL` **&#x20;

****

**`foreigner_v2`      **<mark style="color:orange;">**boolean**</mark>

**`외국인 여부(nullable)`**

* true **** : 외국인
* false : 내국인

다날 본인인증서비스 계약시 외국인 구분기능 추가 요청필요
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

{% swagger-response status="404: Not Found" description="휴대폰 본인인증결과를 찾을 수 없음" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

### Response Model Schema

<details>

<summary>HTTP status 200</summary>

```json
{
  "code": 0,
  "message": "string",
  "response": {
    "imp_uid": "string",
    "merchant_uid": "string",
    "pg_tid": "string",
    "pg_provider": "string",
    "name": "string",
    "gender": "string",
    "birth": 0,
    "birthday": "string",
    "foreigner": true,
    "phone": "string",
    "carrier": "SKT",
    "certified": true,
    "certified_at": 0,
    "unique_key": "string",
    "unique_in_site": "string",
    "origin": "string",
    "foreigner_v2": true
  }
}
```

</details>

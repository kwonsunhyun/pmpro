---
description: 결제 상태값을 기준으로 거래내역을 조회할 수 있는 API입니다.
---

# ⌨ 결제상태기준 복수조회 API

### 결제상태값으로 결제내역을 복수조회 합니다.

{% swagger method="get" path="/payments/status/{payment_status}" baseUrl="https://api.iamport.kr" summary="미결제/결제완료/결제취소/결제실패 상태 별로 검색할 수 있습니다" %}
{% swagger-description %}
검색기간은 최대 **90**일까지이며 to파라메터의 기본값은 현재일자이며 from파라메터의 기본값은 to파라메터 기준으로 90일 전입니다.&#x20;

from/to 파라메터가 없이 호출되면 현재 시점 기준으로 최근 90일 구간에 대한 데이터를 검색하게 됩니다.&#x20;
{% endswagger-description %}

{% swagger-parameter in="path" name="payment_status" type="String" required="true" %}
<mark style="color:red;">**결제상태코드**</mark>** **&#x20;

**-전체 : all**\
\-**미결제 : ready**\
\-**결제완료 : paid**\
\-**결제취소 : cancelled**\
\-**결제실패 : failed**
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="Integer" %}
**페이지번호**

1부터 시작
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="Integer" %}
**페이지 당 조회건수**&#x20;

한 번에 조회할 결제건수\
****(최대 1000건, 기본값 20건)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="from" type="Integer" %}
**검색 시작 시각**

기본값 : to 파라메터 기준으로 90일 전 unix timestamp.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="to" type="Integer" %}
**검색 종료 시각**&#x20;

기본값 : 현재 unix timestamp
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sorting" type="String" %}
**정렬기준**&#x20;

기본값은 -started
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="성공" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="유효하지 않은 payment_status인 경우, 데이터 범위를 넘어선 page인 경우" %}
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

### **주요 요청 파라미터 상세 설명**

> **`sorting`    **<mark style="color:green;">**String**</mark>
>
> **`정렬기준 구분코드` **<mark style="color:green;">****</mark>&#x20;
>
> 마이너스(-) 기호가 앞에 붙으면 내림차순 정렬을 의미합니다.
>
> * \-started : 결제시작시각(결제창오픈시각) 기준 내림차순(DESC) 정렬
> * started : 결제시작시각(결제창오픈시각) 기준 오름차순(ASC) 정렬
> * \-paid : 결제완료시각 기준 내림차순(DESC) 정렬
> * paid : 결제완료시각 기준 오름차순(ASC) 정렬
> * \-updated : 최종수정시각(결제건 상태변화마다 수정시각 변경됨) 기준 내림차순(DESC) 정렬
> * updated : 최종수정시각(결제건 상태변화마다 수정시각 변경됨) 기준 오름차순(ASC) 정렬



### ****



\

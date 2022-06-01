---
description: 세틀뱅크 결제 연동 방법을 안내합니다.
---

# ⌨ 세틀뱅크

### 1. 세틀뱅 PG 설정하기

****[**세틀뱅크 설정**](../undefined/2.-pg/pg/undefined-6.md) **** 페이지의 내용을 참고하여 PG 설정을 진행합니다.

![](<../.gitbook/assets/스크린샷 2022-06-01 오후 4.32.44.png>)

### 2.결제창 요청하기

[JavaScript SDK](../sdk/javascript-sdk/) IMP.**request\_pay**(param, callback)을 호출하여 세틀뱅 결제창을 호출할 수 있습니다. **결제결과**는 PC의 경우 IMP.request\_pay(param, callback) 호출 후 **callback**으로 수신되 모바일의 경우 **m\_redirect\_url**로 리디렉션됩니다.

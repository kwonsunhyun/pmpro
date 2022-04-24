---
description: 본인인증 요청에 필요한 파라미터 정보를 확인합니다.
---

# 💿 본인인증 요청 파라미터

### certification(param, callback) <a href="#certification" id="certification"></a>

> **`merchant_uid`    **<mark style="color:red;">**\***</mark>**    **<mark style="color:green;">**string**</mark>
>
> **주문번호 **<mark style="color:green;">****</mark>&#x20;
>
> 가맹점에서 생성/관리하는 고유 주문번호

> **`min_age`  **<mark style="color:green;">****</mark>**      **<mark style="color:green;">****</mark><mark style="color:purple;">**integer**</mark>
>
> **허용최소 나이 **<mark style="color:purple;">****</mark>&#x20;
>
> 본인인증을 진행할수 있는 최소나이(<mark style="color:red;">다날 PG사 본인인증만 지원</mark>)

> **`name`  **<mark style="color:purple;">****</mark>**      **<mark style="color:green;">**string**</mark>
>
> **고객 이름 **<mark style="color:green;">****</mark>&#x20;
>
> 본인인증 화면 내 이름 필드에 자동입력됨

> **`phone`**  **  **<mark style="color:green;">**string**</mark>
>
> **고객 전화번호 **<mark style="color:green;">****</mark>&#x20;
>
> 본인인증 화면 내 전화번호 필드에 자동입력됨

> **`carrier` **<mark style="color:green;">****</mark> **  **<mark style="color:green;">**string**</mark>
>
> **본인인증 통신사 **<mark style="color:green;">****</mark>&#x20;
>
> 본인인증 화면에서 선택 가능한 통신사 설정
>
> * SKT : `SKT`
> * KT : `KTF`
> * LGU+ : `LGT`
> * 알뜰폰 : `MVNO`

> **`company`**  **  **<mark style="color:green;">**string**</mark>
>
> **서비스 도메인 URL 또는 명칭 **<mark style="color:green;">****</mark>&#x20;
>
> * 서비스의 대표 도메인 URL(예 : https://www.iamport.co.kr) 또는 서비스 명칭(예 : 아임포트)으로 설정
> * 본인인증 동작에 영향을 주지는 않지만, [KISA의 ePrivacy Clean 서비스](https://www.eprivacy.go.kr) 연동을 위해 설정 권장
> * ReactNative / Ionic 등 앱 내 local html을 통해 본 함수가 호출되는 경우, URL 도메인을 인식할 수 없으므로 설정 권장(미 설정 시: `아임포트`)

> **`m_redirect_url`  **<mark style="color:green;">****</mark>**      **<mark style="color:green;">**string**</mark>
>
> **리디렉션 URL **<mark style="color:green;">****</mark>&#x20;
>
> 모바일 환경에서 본인인증 후 리디렉션될 URL
>
> 리디렉션될 때 query string 으로 `imp_uid`, `merchant_uid`, `success` 가 전달됩니다.

> **popup**  **  **<mark style="color:green;">****</mark><mark style="color:orange;">**boolean**</mark>
>
> **팝업 사용여부 **<mark style="color:orange;">****</mark>&#x20;
>
> * PC: `popup` : `true` 옵션이 강제 적용됨
> * 모바일: `popup` : `false` 사용시, `m_redirect_url` 필수 입력

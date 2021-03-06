# Table of contents

* [🧩 아임포트 결제 연동 Docs](README.md)
  * [🚗 GET STARTED](docs/get-started.md)
* [🛫 결제 연동 준비하기](ready/README.md)
  * [🖥 1. 아임포트 회원가입 하기](ready/1..md)
  * [🧷 2. PG정보 설정하기](ready/2.-pg/README.md)
    * [🏢 Payment Gateway](ready/2.-pg/payment-gateway/README.md)
      * [⌨ NHN KCP 설정](ready/2.-pg/payment-gateway/nhn-kcp.md)
      * [⌨ KG 이니시스 설정](ready/2.-pg/payment-gateway/kg.md)
      * [⌨ NICE페이먼츠 설정](ready/2.-pg/payment-gateway/nice.md)
      * [⌨ 토스페이먼츠 설정](ready/2.-pg/payment-gateway/undefined.md)
      * [⌨ KICC 설정](ready/2.-pg/payment-gateway/kicc.md)
      * [⌨ 페이먼트월 설정](ready/2.-pg/payment-gateway/undefined-1.md)
      * [⌨ 다우 설정](ready/2.-pg/payment-gateway/undefined-2.md)
      * [⌨ 다날 설정](ready/2.-pg/payment-gateway/undefined-3.md)
      * [⌨ JTNET 설정](ready/2.-pg/payment-gateway/jtnet.md)
      * [⌨ 세틀뱅크 설정](ready/2.-pg/payment-gateway/undefined-4.md)
      * [⌨ KG모빌리언스 설정](ready/2.-pg/payment-gateway/kg-1.md)
      * [⌨ 스마트로 설정](ready/2.-pg/payment-gateway/undefined-5.md)
      * [⌨ 페이팔 설정](ready/2.-pg/payment-gateway/undefined-6.md)
      * [⌨ 엑심베이 설정](ready/2.-pg/payment-gateway/undefined-7.md)
      * [⌨ 블루월넛 설정](ready/2.-pg/payment-gateway/undefined-8.md)
    * [⛺ 간편 결제사](ready/2.-pg/pg/README.md)
      * [⌨ 카카오페이 설정](ready/2.-pg/pg/undefined.md)
      * [⌨ 토스간편결제 설정](ready/2.-pg/pg/undefined-1.md)
      * [⌨ 네이버페이(결제형) 설정](ready/2.-pg/pg/undefined-2.md)
      * [⌨ 페이코 설정](ready/2.-pg/pg/undefined-3.md)
      * [⌨ 차이 설정](ready/2.-pg/pg/undefined-4.md)
      * [⌨ 알리페이 설정](ready/2.-pg/pg/undefined-5.md)
  * [✔ 3. 연동정보 확인하기](ready/3..md)

## 결제창 연동하기 <a href="#auth" id="auth"></a>

* [🖥 인증결제 연동하기](undefined-1/undefined/README.md)
  * [📒 인증결제 정의](auth/guide/def.md)
  * [🌠 1. 아임포트 라이브러리 추가](undefined-1/undefined/1..md)
  * [💡 2. 객체 초기화 하기](undefined-1/undefined/2..md)
  * [🪧 3. 결제 요청하기](undefined-1/undefined/3..md)
  * [🎁 4. 결제결과 처리하기](undefined-1/undefined/4./README.md)
    * [🪟 iframe 결제창 결과처리](undefined-1/undefined/4./iframe.md)
    * [🖼 redirect 결제창 결과처리](undefined-1/undefined/4./redirect.md)
  * [🔦 5. 결제정보 검증하기](undefined-1/undefined/5..md)
  * [🛬 6. 결제완료 처리하기](undefined-1/undefined/6..md)
* [⏰ 비 인증결제 연동하기](undefined-1/undefined-1/README.md)
  * [🏍 빌링키 결제 요청하기](auth/guide-1/bill/README.md)
    * [🖱 REST API 이용하기](auth/guide-1/bill/rest-api.md)
    * [🛡 PG결제창 이용하기](auth/guide-1/bill/pg.md)
  * [💳 카드정보를 이용한 키인결제](undefined-1/undefined-1/page-1.md)
  * [🪧 빌링키를 이용한 정기결제](auth/guide-1/undefined.md)
* [💸 결제취소(환불) 연동하기](undefined-1/undefined-2.md)
  * [💷 가상계좌 환불하기](auth/guide-2/refund.md)

## 결제결과  연동하기 <a href="#result" id="result"></a>

* [⚒ 웹훅(Webhook) 연동하기](result/webhook.md)

## 기타 서비스 연동하기 <a href="#etc" id="etc"></a>

* [📱 휴대폰 본인인증 연동하기](etc/phone/README.md)
  * [📔 1. 본인인증 준비하기](etc/phone/1..md)
  * [🥏 2. 본인인증창 호출하기](etc/phone/2..md)
  * [🚚 3. 인증 완료정보 전달하기](etc/phone/3..md)
  * [🤹 4. 인증정보 조회 및 활용하기](etc/phone/4..md)
* [🚚 통합인증 연동하기](etc/all/README.md)
  * [📒 통합인증 준비하기](etc/all/undefined.md)
  * [🥏 통합인증 요청하기](etc/all/undefined-1.md)
  * [🚚 인증 완료정보 전달하기](etc/all/undefined-2.md)
  * [🤹 인증정보 조회 및 활용하기](etc/all/undefined-3.md)
* [💳 신용카드 본인인증 연동](etc/credit-auth/README.md)
  * [📒 1. 본인인증 준비하기](etc/credit-auth/1..md)
  * [🥏 2. 본인인증 요청하기](etc/credit-auth/2..md)
  * [🚚 3. 인증 완료정보 전달하기](etc/credit-auth/3..md)
  * [🤹 4. 인증정보 조회 및 활용하기](etc/credit-auth/4..md)
* [💻 결제 URL 생성하기](etc/url.md)
* [🛩 버짓핸들러 연동하기](etc/budget.md)
* [📟 네이티브 모바일 SDK](etc/sdk.md)

## TIP

* [🌽 결제금액 면세 적용방법](tip/tax.md)
* [✅ 오픈 전 체크사항](tip/chk.md)
* [🔏 Confirm Process](tip/confirm-process.md)
* [🎼 아임포트 결제 FLOW](tip/flow.md)
* [🎈 Agency & Tier 란?](tip/agency-and-tier.md)
* [📦 PG사별 빌링키 획득 규칙](tip/pg.md)
* [🏦 PG사별 은행코드표](tip/pg-1.md)
* [🧾 PG사 코드표](tip/pg-2.md)
* [🚚 택배사 코드표](tip/code.md)
* [🪧 리디렉션이란?](tip/redirect.md)
* [📰 PG사 오류코드](tip/pg-3.md)

## 관리자 콘솔 사용하기 <a href="#console" id="console"></a>

* [🎡 관리자 콘솔 가이드](console/guide/README.md)
  * [전자결제 신청](console/guide/reg.md)
  * [내 식별코드, API Keys](console/guide/api-keys.md)
  * [관리자 및 하위 상점 계정 관리](console/guide/account.md)
  * [결제 연동 하기](console/guide/connect.md)
  * [결제 내역](console/guide/list.md)
* [💻 복수 PG설정 및 사용하기](console/pg.md)

## API

* [📋 아임포트 API 소개](api/api.md)
* [🖇 REST API Access Token](api/rest-api-access-token.md)
* [💳 결제관련 API](api/api-1/README.md)
  * [⌨ 결제취소 API](api/api-1/api.md)
  * [⌨ 결제내역 단건조회 API](api/api-1/api-1.md)
  * [⌨ 결제내역 복수조회 API](api/api-1/api-2.md)
  * [⌨ 결제상태기준 복수조회 API](api/api-1/api-3.md)
  * [⌨ 결제 복수조회(주문All) API](api/api-1/all-api.md)
  * [⌨ 결제 복수조회(주문UQ) API](api/api-1/uq-api.md)
  * [⌨ 결제 상세내역 조회 API](api/api-1/api-4.md)
  * [⌨ 빌링키 결제 복수조회 API](api/api-1/api-5.md)
  * [⌨ 결제금액 사전등록 API](api/api-1/api-6.md)
  * [⌨ 결제금액 단건 수정 API](api/api-1/api-7.md)
  * [⌨ 결제금액 단건조회](api/api-1/undefined.md)
* [📝 빌링키 관리 API](api/api-2/README.md)
  * [⌨ 빌링키 발급 API](api/api-2/api-1.md)
  * [⌨ 빌링키 삭제 API](api/api-2/api.md)
  * [⌨ 빌링키 정보 단건조회 API](api/api-2/api-2.md)
  * [⌨ 빌링키 정보 복수조회 API](api/api-2/api-3.md)
  * [⌨ 빌링키 결제예약 조회 API](api/api-2/api-4.md)
* [🧭 정기결제 관련 API](api/api-3/README.md)
  * [⌨ 결제 예약 API](api/api-3/api.md)
  * [⌨ 결제 예약취소 API](api/api-3/api-1.md)
  * [⌨ 결제예약 복수조회 API](api/api-3/api-2.md)
  * [⌨ 결제예약 단건조회 API](api/api-3/api-3.md)
  * [⌨ 결제예약 복수조회(빌키) API](api/api-3/api-4.md)
* [🪂 비 인증 결제관련 API](api/api-4/README.md)
  * [⌨ 비 인증 결제(빌링키) API](api/api-4/api.md)
  * [⌨ 비 인증 결제(일회성) API](api/api-4/api-1.md)
* [🇺🇲 해외PG 관련 API](api/pg-api/README.md)
  * [⌨ 페이먼트월 배송등록 API](api/pg-api/api.md)
* [👮♂ 본인인증 관련 API](api/api-5/README.md)
  * [⌨ 본인인증 결과조회 API](api/api-5/api.md)
  * [⌨ 본인인증 정보삭제 API](api/api-5/api-1.md)
  * [⌨ 본인인증 요청 API](api/api-5/api-3.md)
  * [⌨ 본인인증 완료 API](api/api-5/api-2.md)
* [🎫 간편결제 서비스 API](api/api-6.md)
  * [🧽 카카오페이](api/api-6/undefined/README.md)
    * [⌨ 주문내역 조회 API](api/api-6/undefined/api.md)
  * [🛩 KCP Quick Pay](api/api-6/kcp-quick-pay/README.md)
    * [⌨ 구매자 정보 단건 삭제 API](api/api-6/kcp-quick-pay/api.md)
  * [🧰 페이코](api/api-6/undefined-1/README.md)
    * [⌨ 주문상태 단건 수정 API](api/api-6/undefined-1/api.md)
  * [📗 네이버페이 결제형](api/api-6/undefined-2/README.md)
    * [⌨ 에스크로 주문확정 API](api/api-6/undefined-2/api.md)
    * [⌨ 포인트 적립 API](api/api-6/undefined-2/api-1.md)
    * [⌨ 현금영수증 발급 가용액 조회 API](api/api-6/undefined-2/api-2.md)
* [🏦 에스크로 관련 API](api/api-7/README.md)
  * [⌨ 배송정보 단건조회 API](api/api-7/api.md)
  * [⌨ 배송정보 단건등록 API](api/api-7/api-1.md)
  * [⌨ 배송정보 단건수정 API](api/api-7/api-2.md)
* [💵 현금영수증 API](api/api-8/README.md)
  * [⌨ 아임포트 발급분 취소 API](api/api-8/api.md)
  * [⌨ 발급내역 단건 조회 API](api/api-8/api-1.md)
  * [⌨ 현금영수증 단건발급 API](api/api-8/api-2.md)
  * [⌨ 외부 발급분 취소 API](api/api-8/api-3.md)
  * [⌨ 외부 발급내역 단건 조회 API](api/api-8/api-4.md)
  * [⌨ 현금영수증 발급(외부) API](api/api-8/api-5.md)
* [🏛 가상계좌 관련 API](api/api-9/README.md)
  * [⌨ 가상계좌 발급 API](api/api-9/api.md)
  * [⌨ 가상계좌 발급취소 API](api/api-9/api-1.md)
  * [⌨ 가상계좌 발급정보 수정 API](api/api-9/api-2.md)
  * [⌨ 예금주 조회 API](api/api-9/api-3.md)
* [🍶 기타 API](api/api-10/README.md)
  * [🎽 베네피아 포인트](api/api-10/undefined/README.md)
    * [⌨ 포인트 단건조회 API](api/api-10/undefined/api.md)
    * [⌨ 포인트 결제 요청](api/api-10/undefined/undefined.md)
  * [🏪 편의점 결제](api/api-10/undefined-1/README.md)
    * [⌨ 수납번호 발급 API](api/api-10/undefined-1/api.md)
    * [⌨ 수납취소 API](api/api-10/undefined-1/api-1.md)
  * [🗃 기관코드 조회](api/api-10/undefined-2/README.md)
    * [⌨ 카드사코드 전체조회 API](api/api-10/api.md)
    * [⌨ 카드사명 단건조회 API](api/api-10/api-1.md)
    * [⌨ 은행코드 전체조회 API](api/api-10/api-2.md)
    * [⌨ 은행명 단건조회 API](api/api-10/api-3.md)
  * [🛖 PG 정보](api/api-10/pg/README.md)
    * [⌨ PG MID 복수조회 API](api/api-10/pg/pg-mid-api.md)

## SDK

* [📚 Javascript SDK](sdk/javascript-sdk/README.md)
  * [💿 결제요청 파라미터](sdk/javascript-sdk/undefined.md)
  * [📀 결제응답 파라미터](sdk/javascript-sdk/undefined-1.md)
  * [💿 본인인증 요청 파라미터](sdk/javascript-sdk/undefined-2.md)
  * [📀 본인인증 결과 파라미터](sdk/javascript-sdk/undefined-3.md)
  * [✏ SDK Release Note](sdk/javascript-sdk/sdk-release-note.md)

## FAQ

* [⁉ 자주 묻는 질문](faq/undefined.md)

## 🔑 PG사별 결제 연동 가이드

* [🏢 Payment Gateway](pg/payment-gateway/README.md)
  * [⌨ NHH KCP](pg/nhh-kcp.md)
  * [⌨ KG 이니시스](pg/inicis.md)
  * [⌨ 토스페이먼츠](pg/toss.md)
  * [⌨ NICE페이먼츠](pg/nice.md)
  * [⌨ KICC](pg/payment-gateway/kicc.md)
  * [⌨ 다우(페이조아)](pg/payment-gateway/undefined.md)
    * [📍 페이조아 유의사항](pg/payment-gateway/undefined/undefined.md)
  * [⌨ KG모빌리언스](pg/payment-gateway/kg.md)
  * [⌨ 페이먼트월](pg/payment-gateway/undefined-1.md)
  * [⌨ 다날](pg/payment-gateway/undefined-2.md)
  * [⌨ 세틀뱅크](pg/payment-gateway/undefined-3.md)
  * [⌨ JTNET](pg/jtnet.md)
  * [⌨ 스마트로](pg/payment-gateway/undefined-4.md)
  * [⌨ 페이팔](pg/payment-gateway/undefined-5.md)
  * [⌨ 엑심베이](pg/payment-gateway/undefined-6.md)
  * [⌨ 블루월넛](pg/payment-gateway/undefined-7.md)
* [⛺ 간편 결제사](pg/simple/README.md)
  * [⌨ 네이버페이(결제형)](pg/simple/undefined.md)
  * [⌨ 카카오페이](pg/simple/undefined-1.md)
  * [⌨ 페이코](pg/simple/undefined-2.md)
  * [⌨ 차이 간편결제](pg/simple/undefined-3.md)
  * [⌨ 알리페이](pg/simple/undefined-4.md)
  * [⌨ 토스 간편결제](pg/simple/undefined-5.md)

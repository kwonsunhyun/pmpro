# Table of contents

* [🧩 차이포트 결제 연동 Docs](README.md)
  * [🚗 GET STARTED](docs/get-started.md)
* [🛫 결제 연동 준비하기](undefined/README.md)
  * [🖥 1. 아임포트 회원가입 하기](undefined/1..md)
  * [🧷 2. PG정보 설정하기](undefined/2.-pg/README.md)
    * [🕹 PG사별 설정](undefined/2.-pg/pg/README.md)
      * [⌨ KG 이니시스 설정하기](undefined/2.-pg/pg/kg.md)
      * [⌨ 토스페이먼트 설정하기](undefined/2.-pg/pg/undefined.md)
      * [⌨ NICE 설정하기](undefined/2.-pg/pg/nice.md)
      * [⌨ 페이먼트월 설정하기](undefined/2.-pg/pg/undefined-1.md)
      * [⌨ NHN KCP 설정하기](undefined/2.-pg/pg/nhn-kcp.md)
      * [⌨ 토스간편결제 설정하기](undefined/2.-pg/pg/undefined-2.md)
      * [⌨ 나이스페이먼츠 설정하기](undefined/2.-pg/pg/undefined-3.md)
  * [✔ 3. 연동정보 확인하기](undefined/3..md)

## 결제창 연동하기

* [🖥 인증결제 연동하기](undefined-1/undefined/README.md)
  * [📒 인증결제 정의](undefined-1/undefined/undefined.md)
  * [🌠 1. 차이포트 라이브러리 추가](undefined-1/undefined/1..md)
  * [💡 2. 객체 초기화 하기](undefined-1/undefined/2..md)
  * [🪧 3. 결제 요청하기](undefined-1/undefined/3..md)
  * [🎁 4. 결제결과 처리하기](undefined-1/undefined/4./README.md)
    * [🪟 iframe 결제창 결과처리](undefined-1/undefined/4./iframe.md)
    * [🖼 redirect 결제창 결과처리](undefined-1/undefined/4./redirect.md)
  * [🔦 5. 결제정보 검증하기](undefined-1/undefined/5..md)
  * [🛬 6. 결제완료 처리하기](undefined-1/undefined/6..md)
* [⏰ 비 인증결제 연동하기](undefined-1/undefined-1/README.md)
  * [🏍 빌링키 기반 결제 요청하기](undefined-1/undefined-1/undefined.md)
    * [🖱 REST API 이용하기](undefined-1/undefined-1/undefined/rest-api.md)
    * [🛡 PG결제창 이용하기](undefined-1/undefined-1/undefined/pg.md)
  * [💳 카드정보를 이용한 키인결제](undefined-1/undefined-1/page-1.md)
  * [🪧 빌링키를 이용한 정기결제](undefined-1/undefined-1/undefined-1.md)
* [💸 결제취소(환불) 연동하기](undefined-1/undefined-2.md)
  * [💷 가상계좌 환불하기](undefined-1/undefined-2/undefined.md)

## 결제결과  연동하기

* [⚒ 웹훅(Webhook) 연동하기](undefined-2/webhook.md)

## 기타 서비스 연동하기

* [📱 휴대폰 본인인증 연동하기](undefined-3/undefined.md)
  * [📔 1. 본인인증 준비하기](undefined-3/undefined/1..md)
  * [🥏 2. 본인인증창 호출하기](undefined-3/undefined/2..md)
  * [🚚 3. 인증 완료정보 전달하기](undefined-3/undefined/3..md)
  * [🤹 4. 인증정보 조회 및 활용하기](undefined-3/undefined/4..md)
* [💳 신용카드 본인인증 연동하기](undefined-3/undefined-2.md)
  * [📒 1. 본인인증 준비하기](undefined-3/undefined-2/1..md)
  * [🥏 2. 본인인증 요청하기](undefined-3/undefined-2/2..md)
  * [🚚 3. 인증 완료정보 전달하기](undefined-3/undefined-2/3..md)
  * [🤹 4. 인증정보 조회 및 활용하기](undefined-3/undefined-2/4..md)
* [💻 결제 URL 생성하기](undefined-3/url.md)
* [🚚 통합인증 연동하기](undefined-3/undefined-1.md)
* [🛩 버짓핸들러 연동하기](undefined-3/undefined-3.md)

## TIP

* [🌽 결제금액 면세 적용방법](tip/undefined.md)
* [✅ 오픈 전 체크사항](tip/undefined-1.md)
* [🔏 Confirm Process](tip/confirm-process.md)
* [🎼 아임포트 결제 FLOW](tip/flow.md)
* [🎈 Agency & Tier 란?](tip/agency-and-tier.md)
* [🏦 PG사별 은행코드표](tip/pg.md)
* [🧾 PG사 코드표](tip/pg-1.md)

## 관리자 콘솔 사용하기

* [💱 테스트 결제 모드 설정하기](undefined-4/undefined.md)
* [💻 복수 PG설정 및 사용하기](undefined-4/pg.md)

## API

* [📋 차이포트 API 소개](api/api.md)
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
* [👮♂ 본인인증 관련 API](api/api-5/README.md)
  * [⌨ 본인인증 결과조회 API](api/api-5/api.md)
  * [⌨ 본인인증 정보삭제 API](api/api-5/api-1.md)
  * [⌨ 본인인증 완료 API](api/api-5/api-2.md)
  * [⌨ 본인인증 요청 API](api/api-5/api-3.md)
* [🎫 간편결제 서비스 API](api/api-6.md)
* [💵 현금영수증 API](api/api-7.md)
  * [⌨ 차이포트 발급분 취소 API](api/api-7/api.md)
  * [⌨ 발급내역 단건 조회 API](api/api-7/api-1.md)
  * [⌨ 현금영수증 단건발급 API](api/api-7/api-2.md)
  * [⌨ 외부 발급분 취소 API](api/api-7/api-3.md)
  * [⌨ 외부 발급내역 단건 조회 API](api/api-7/api-4.md)
  * [⌨ 현금영수증 발급(외부) API](api/api-7/api-5.md)
* [🏛 가상계좌 관련 API](api/api-8/README.md)
  * [⌨ 가상계좌 발급 API](api/api-8/api.md)
  * [⌨ 가상계좌 발급취소 API](api/api-8/api-1.md)
  * [⌨ 가상계좌 발급정보 수정 API](api/api-8/api-2.md)
  * [⌨ 예금주 조회 API](api/api-8/api-3.md)
* [🍶 기타 API](api/api-9.md)
  * [⌨ 카드사코드 조회 API](api/api-9/api.md)
  * [⌨ 카드사명 조회 API](api/api-9/api-1.md)
  * [⌨ 은행코드 조회 API](api/api-9/api-2.md)
  * [⌨ 은행명 조회 API](api/api-9/api-3.md)

## SDK

* [📚 Javascript SDK](sdk/javascript-sdk/README.md)
  * [💿 결제요청 파라미터](sdk/javascript-sdk/undefined.md)
  * [📀 결제응답 파라미터](sdk/javascript-sdk/undefined-1.md)
  * [💿 본인인증 요청 파라미터](sdk/javascript-sdk/undefined-2.md)
  * [📀 본인인증 결과 파라미터](sdk/javascript-sdk/undefined-3.md)
  * [✏ SDK Release Note](sdk/javascript-sdk/sdk-release-note.md)

## FAQ

* [⁉ 자주 묻는 질문](faq/undefined.md)

## 🔑 PG사별 결제창 연동 가이드

* [⌨ NHH KCP](pg/nhh-kcp.md)
* [⌨ NICE](pg/nice.md)
* [⌨ TOSS](pg/toss.md)
* [⌨ INICIS](pg/inicis.md)

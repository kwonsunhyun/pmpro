---
description: 결제가 이루어진 거래내역을 조회할 수 있는 메뉴입니다.
---

# 결제 내역

## 결제내역 체계

결제내역 화면에서는 결제가 이루어진 내역을 확인할 수 있는 화면입니다.

* 결제가 시도된 날짜의 범위를 필터할 수 있는 캘린더 필터
* 결제내역의 특정 데이터를 지정하여 혹은 미지정시 전체 데이터를 통합검색을 할수 있는 통합검색
* 결제 상태, 수단, 대행사, 유형, 모드 를 지정하여 검색 할 수 있는 필터
* 검색된 내역 결과를 상태별로 통계화 한 상태별 결제건
* 결제 상태, 고객정보, 결제 수단, 결제 대행사, 결제 금액, 구분, 요청시각, 완료시각을 확인할 수 있는 결제내역 리스트 뷰
* 해당 내역의 특정 결제건의 우측 코너를 클릭하여 MID, UID 복사 기능
* 해당 내역의 특정 결제건을 클릭하여 확인할 수 있는 결제내역 상세정보
* 해당 내역의 특정 결제건을 클릭하여 수행 할 수 있는 결제 취소 기능
* 해당 내역의 특정 결제건을 클릭하여 수행 할 수 있는 웹훅 재전송 기능
* 검색된 내역의 총 거래액 - 총 환불액의 계산을 통하여 통화별로 확인 할 수 있는 총 매출액 기능
* 기본 결제내역 값들과 추가적으로 고객정보, 결제 대행사 정보, 카드결제 정보, 계좌결제 정보 를 선택하여 내역을 다운받을 수 있는 엑셀 다운로드 기능

위 기능들로 구성되어 있는 화면입니다.\




## 캘린더 필터&#x20;

![](<../../.gitbook/assets/Screen Shot 2022-06-20 at 5.23.19 PM.png>)



* 결제 요청시각 기준으로 검색하고 싶은 결제 내역의 시작 날짜 및 시각과 끝 날짜 및 시각과 끝을 지정 합니다.
  * 결제 요청이란 가맹점의 고객이 결제를 시도한 시점입니다.
  * 따라서 결제 환불 및 완료 시간 기준으로는 해당 날짜 기간안 이후로 벗어 날 수 있습니다.
* 년, 월, 일, 시, 분 단위까지 지정하실 수 있습니다.
* 편의를 위해 오늘, 어제, 과거 7일, 30일, 90일 버튼을 누르셔서 빠르게 세팅 하실 수 있습니다.
* 캘린더 UI를 통해서가 아니라 직접 기간을 입력하셔서 사용하실 수 있습니다.

## 통합 검색

![](<../../.gitbook/assets/Screen Shot 2022-06-20 at 5.36.36 PM.png>)



* 결제내역의 특정값을 지정하시거나 모든 결제관련 값에 대해서 직접 입력하신 값을 검색하는 기능입니다.
* 통합검색 필터는
  * 아임포트 거래번호
  * 가맹점 거래번호
  * 카드사 승인번호
  * 고객 이름
  * 고객 휴대폰번호
  * 고객 이메일
  * 결제대행사 승인번호
  * 카드번호
  * 상점아이디
  * 결제환경
  * 실시간 계좌 은행
  * 가상계좌 은행
  * 계좌번호
  * 입금자명
  * 현금영수증 발급번호
  * 고객 주소
  * 취소 사유
  * 결제환경 상세
  * 주문명

으로 이루어져 있습니다.

* 검색 로직은 like %value 입니다. 즉 값의 맨 앞에서부터 일치하는 값을 리턴합니다.
  * 추후에 주문명과 고객 주소는 like %value%로 업데이트 될 예정입니다.
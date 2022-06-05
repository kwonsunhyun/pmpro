# ⌨ 토스간편결제 설정

### <mark style="color:blue;">**STEP 01.**</mark>** 서비스 신청**&#x20;

**아임포트 로그인 >** [**https://www.iamport.kr/**](https://www.iamport.kr/) **메인 "지금 시작하기" 클릭  > PG사 선택 "토스간편결제" 선택 후 정보기재 > 신청서 제출하기**

### <mark style="color:blue;">**STEP 0**</mark><mark style="color:blue;">**2**</mark><mark style="color:blue;">**.**</mark>** PG설정방법**

아임포트 관리자콘솔([https://admin.iamport.kr/](https://admin.iamport.kr/)) 로그인 > 시스템설정 > PG설정(일반결제 및 정기결제) 에서 PG사 "\[간편결제]토스" 선택 후 테스트 모드 \[ON]상태에서 하단 \[전체저장] 클릭

* 테스트 상점아이디 : tosstest
* 테스트 apiKey : sk\_test\_w5lNQylNqa5lNQe013Nq

{% hint style="info" %}
**참고** __&#x20;

이미 기본PG설정하여 이용중이신 경우, '**+PG사 추가**' 클릭하시어 추가PG로 설정 바랍니다.

\
실운영모드는 테스트모드 \[<mark style="color:red;">**OFF**</mark>] 후 토스간편결제에서 발급된 실상점연동정보로 세팅 후 저장하시어 최종적으로 결제 테스트 진행 후 서비스 이용 바랍니다.
{% endhint %}

![설정 화면 예시 - 테스트모드](https://mail.google.com/mail/u/0?ui=2\&ik=eabc50b472\&attid=0.1\&permmsgid=msg-f:1731136926968037438\&th=18063bdcf57dc03e\&view=fimg\&fur=ip\&sz=s0-l75-ft\&attbid=ANGjdJ-kFDi3k4WhSlWg5TFIhz\_3vubRPibq7xYNaMqpBVBpedhbSQarjdiWPePxqEbiqbG4jWk9QD-aMXj0HGYXzM-nJNRaj7-JkMzbS1bjrV3ahjRKGS\_jcdTlTaY\&disp=emb\&realattid=ii\_ky84j8az0)

### 연동참고 사항

#### Toss 간편결제 동작 인터페이스

* PC결제 : 팝업창을 통한 결제 진행
* 모바일결제 : 페이지 리디렉션을 통한 결제 진행

#### Toss 간편결제 내장 결제수단

* 신용카드 : Toss 앱 내 등록된 '카드'로 결제 => 아임포트에서는 pay\_method : card 로 인식
* 계좌이체 : Toss 앱 내 연결된 '계좌'로 결제 => 아임포트에서는 pay\_method : trans 로 인식&#x20;

#### 결제 후 저장되는 '승인'에 대한 extension 정보 ( 정산금액 관련 )

* paidPoint : 승인금액 중 토스머니 차감액
* discountedAmount : 승인금액 중 할인적용 금액
* paidAmount : 승인금액 중 주결제수단(신용카드/계좌이체) 승인금액&#x20;

#### 환불 후 저장되는 매 '환불' 건에 대한 extension 정보 ( 정산금액 관련 )

* refundedPoint : 해당환불금액 중 토스머니 환불액
* refundedDiscountAmount : 해당환불금액 중 취소된 할인금액
* refundedPaidAmount : 해당환불금액 중 주결제수단(신용카드/계좌이체) 환불금액

\

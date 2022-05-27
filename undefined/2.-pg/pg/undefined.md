---
description: 토스페이먼츠 설정방법을 안내합니다.
---

# ⌨ 토스페이먼츠 설정하기

### **\[토스페이먼츠\_PG설정방법\_테스트모드]**

**1. 아임포트관리자콘솔(**[**https://admin.iamport.kr**](https://admin.iamport.kr/)**) 로그인(또는 회원가입) 후 > 시스템 설정 > PG설정(일반결제 및 정기결제) > PG사 "토스페이먼츠" 선택하시고 테스트모드 \[ON] 상태에서 \[전체저장] 버튼을 클릭 해 주세요.**\
\
**- 참고 : '실운영모드'는 토스페이먼츠와 계약 후 발급된 연동상점정보(MID/ MertKey)** **발급 후 직접 테스트모드\[OFF]상태에서 세팅 해 주시면 됩니다.**

![토스페이먼츠\_테스트모드 설정 화면 예시](<../../../.gitbook/assets/image (10).png>)

### **2. 아임포트 웹훅(Notification URL) 설정방법**&#x20;

아임포트 Webhook을 사용함으로써 아임포트 서버에 저장된 데이터를 서버에 동기화하고 네트워크 불안정성을 보완할 수 있습니다.&#x20;

#### - 설정 방법 : 웹훅 설정 매뉴얼 [https://docs.iamport.kr/tech/webhook](https://docs.iamport.kr/tech/webhook) 링크 내용 참고하시어 아임포트관리자페이지 > 시스템설정 > 웹훅(Notification) 설정 메뉴에서 "웹훅(Notification) 발송 공통 URL" 항목에 설정 해 줍니다.

![웹훅 설정 화면 예시](<../../../.gitbook/assets/image (6).png>)

{% hint style="info" %}
**토스페이먼츠(LGU+) 일반** **인증결제 연동 샘플페이지**&#x20;

****[https://github.com/iamport/iamport-manual/blob/master/%EC%9D%B8%EC%A6%9D%EA%B2%B0%EC%A0%9C/sample/uplus.md](https://github.com/iamport/iamport-manual/blob/master/%EC%9D%B8%EC%A6%9D%EA%B2%B0%EC%A0%9C/sample/uplus.md)
{% endhint %}

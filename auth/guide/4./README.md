---
description: 결제결과를 안전하게 저장할 수 있는 가이드 입니다.
---

# 🎁 4. 결제결과 처리하기

#### 결제창이 활성화되는 방식에 따라 결제결과를 획득하는 방법이 상이합니다. 일반적으로 PC 환경에서는 iframe 방식으로 결제창이 활성화되며 모바일 환경에서는 새로운페이지로 리다이렉트 되어 결제창이 활성화 됩니다.

결제가 정상적으로 완료되면 결제창 형태에 따라 아래와 같이 결제결과를 받아 볼 수 있습니다.

|    iframe 형태    |         팝업형태         |
| :-------------: | :------------------: |
| **callback 함수** | **m\_redirect\_url** |

자세한 가이드는 아래 링크를 따라가보세요

{% content-ref url="iframe.md" %}
[iframe.md](iframe.md)
{% endcontent-ref %}

{% content-ref url="redirect.md" %}
[redirect.md](redirect.md)
{% endcontent-ref %}

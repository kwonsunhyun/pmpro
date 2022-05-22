---
description: 아임포트 REST API 를 이용하여 손쉽게 빌링키를 획득할수 있습니다.
---

# 🖱 REST API 이용하기

아임포트 REST API 를 이용하여 빌링키를 획득하여 결제를 요청할 수 있습니다. 고객 카드정보를 이용하여 빌링키 발급을 요청하면 아임포트 서버가 PG사의 API를 호출하여 빌링키를 발급받습니다. 이 과정에서 카드정보는 기록되지 않습니다.이 방식은 다음과 같은 특징이 있습니다.

* **장점**: 가맹점이 원하는 형태의 화면으로 **카드정보 입력란을 커스터마이징**할 수 있다.
* **단점**: **개인정보 이용약관**을 명시해야 하며 PG사 및 카드사 심사가 까다롭고 개인정보 유출에 유의해야 합니다.

#### 가맹점 UI/UX 친화적인 결제 환경을 계획하고 계시다면 API 연동 개발을 선택하시면 됩니다.

### <mark style="color:blue;">**STEP 01.**</mark> 카드 정보 입력받기

카드 정보를 입력하는 필드들을 다음과 같이 작성합니다. 요청 시 **customer\_uid**를 저장 할 히든필드를 작성합니다. 법인카드(개인명의로 발급된 _기명카드_ 제외)의 경우 `birth` 파라미터에 \_사업자번호 10자리\_를 입력하시면 됩니다. 결제하기 버튼 클릭 시 입력 값들과 customer\_uid로 `/subscription/issue-billing`에 대해`POST`요청이 호출되는 예제입니다.&#x20;

{% hint style="info" %}
**customer\_uid 란?**

PG사가 발급한 빌링키와 1:1로 맵핑되는 가맹점이 지정한 고유값입니다. customer\_uid 는 카드번호 단위로구분되서 저장되어야 합니다.

예) **홍길동** 고객이 **A카드** 빌링키를 요청하는 경우 customer\_uid는 **회원별 카드번호 단위**로 고유하게 발급되어야 합니다.
{% endhint %}

{% hint style="danger" %}
이전 빌링키 발급에 사용된 customer\_uid 를 재 사용하는 경우 가장 마지막 빌링키 발급에 사용된 카드번호 빌링키로 대체됩니다.(**기존 카드에 맵핑된 빌링키는 삭제처리**)
{% endhint %}

{% hint style="info" %}
**빌링키 발급을 위한 카드정보**

* **카드번호**
* **유효기간**
* **생년월일**
* **비밀번호 앞 두자리**
{% endhint %}

{% tabs %}
{% tab title="HTML" %}
{% code title="client-side" %}
```html
<form action="{빌링키 발급 요청을 받을 서비스 URL}", method="post">
  <!--예: https://www.myservice.com/subscription/issue-billing-->
    <div>
        <label for="card_number">카드 번호 XXXX-XXXX-XXXX-XXXX</label>
        <input id="card_number" type="text" name="card_number">
    </div>
    <div>
        <label for="expiry">카드 유효기간 YYYY-MM</label>
        <input id="expiry" type="text" name="expiry">
    </div>
    <div>
        <label for="birth">생년월일 YYMMDD</label>
        <input id="birth" type="text" name="birth">
    </div>
    <div>
        <label for="pwd_2digit">카드 비밀번호 앞 두자리 XX</label>
        <input id="pwd_2digit" type="text" name="pwd_2digit">
    </div>
    <input hidden type="text" value="gildong_0001_1234" name="customer_uid">
    <input type="submit" value="결제하기">
  </form>
```
{% endcode %}
{% endtab %}

{% tab title="React.js" %}
{% code title="client-side" %}
```jsx
// React.js
  class CardForm extends React.Components {
    constructor(props) {
      super(props);
      this.state = {
        cardNumber: "",
        expiry: "",
        birth: "",
        pwd2Digit: "",
        customer_uid: "gildong_0001_1234",
      };
    }
    ...
    handleInputChange = (event) => {
      const { value, name } = event.target;
      this.setState({
        [name]: value,
      });
    };
    ...
    handleFormSubmit = (event) => {
      event.preventDefault();
      const { cardNumber, expiry, birth, pwd2Digit, customer_uid } = this.state;
      axios({
        // 예: https://www.myservice.com/subscription/issue-billing
        url: "{빌링키 발급 요청을 받을 서비스 URL}", 
        method: "post",
        data: {
          cardNumber,
          expiry,
          birth,
          pwd2Digit,
          customer_uid,
        }
      }).then(rsp => {
        ...
      });
    };
    ...
    render() {
      const { cardNumber, expiry, birth, pwd2Digit } = this.state;
      return (
        <form onSubmit={this.handleFormSubmit}>
          <label>
            카드 번호
            <input type="text" name="cardNumber" value={cardNumber} onChange={this.handleInputChange} />
          </label>
          <label>
            카드 유효기간
            <input type="text" name="expiry" value={expiry} onChange={this.handleInputChange} />
          </label>
          <label>
            생년월일
            <input type="text" name="birth" value={birth} onChange={this.handleInputChange} />
          </label>
          <label>
            카드 비밀번호 앞 두자리
            <input type="text" name="pwd2Digit" value={pwd2Digit} onChange={this.handleInputChange} />
          </label>
          <input type="submit" value="결제하기" />
        </form>
      )
    }
  }
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% embed url="https://codepen.io/chaiport/pen/mdpWYqg" %}

### <mark style="color:blue;">**STEP 02.**</mark> 카드 정보 추출하기

카드 정보를 전달받을 API endpoint를 작성하고 요청에 담긴 카드 정보를 추출합니다.`/subscription/issue-billing`에 대한 `POST`요청을 처리하는 **API endpoint**의 예제입니다.

{% tabs %}
{% tab title="Node.js" %}
{% code title="server-side" %}
```javascript
// "/subscription/issue-billing"에 대한 POST 요청을 처리
  app.post("/subscriptions/issue-billing", async (req, res) => {
    try {
      const {
        card_number, // 카드 번호
        expiry, // 카드 유효기간
        birth, // 생년월일
        pwd_2digit, // 카드 비밀번호 앞 두자리,
        customer_uid, // 카드(빌링키)와 1:1로 대응하는 값
      } = req.body; // req의 body에서 카드정보 추출
      ...
    } catch (e) {
      res.status(400).send(e);
    }
  });
```
{% endcode %}
{% endtab %}
{% endtabs %}

### <mark style="color:blue;">**STEP 03.**</mark>  빌링키 발급 요청 및 응답 처리하기

당사가 제공하는 [**빌링키 발급 REST API** ](../../../api/api-4/)를 통해 빌링키 발급을 요청하고 결과값에 따라 응답을 반환하는 예제입니다.

{% tabs %}
{% tab title="Node.js" %}
{% code title="server-side" %}
```javascript
// "/subscription/issue-billing"에 대한 POST 요청을 처리
    app.post("/subscriptions/issue-billing", async (req, res) => {
      try {
        const {
          card_number,  // 카드 번호
          expiry,       // 카드 유효기간
          birth,        // 생년월일
          pwd_2digit,   // 카드 비밀번호 앞 두자리
          customer_uid, // 카드(빌링키)와 1:1로 대응하는 값
        } = req.body;   // req의 body에서 카드정보 추출
        ...
        // 인증 토큰 발급 받기
        const getToken = await axios({
          url: "https://api.iamport.kr/users/getToken",
          method: "post",          // POST method
          headers: { "Content-Type": "application/json" }, 
          data: {
            imp_key: "imp_apikey", // REST API 키
            imp_secret: "ekKoeW8RyKuT0zgaZsUtXXTLQ4AhPFW3ZGseDA6bkA5lamv9OqDMnxyeB9wqOsuO9W3Mx9YSJ4dTqJ3f" 
          }
        });
        const { access_token } = getToken.data.response; // 인증 토큰
        ...
        // 빌링키 발급 요청
        const issueBilling = await axios({
          url: \`https://api.iamport.kr/subscribe/customers/\${customer_uid}\`,
          method: "post",
          // 인증 토큰 Authorization header에 추가
          headers: { "Authorization": access_token }, 
          data: {
            card_number, // 카드 번호
            expiry,      // 카드 유효기간
            birth,       // 생년월일
            pwd_2digit,  // 카드 비밀번호 앞 두자리
          }
        });
        ...
        const { code, message } = issueBilling.data;
        if (code === 0) { // 빌링키 발급 성공
          res.send({ status: "success", message: "Billing has successfully issued" });
        } else {          // 빌링키 발급 실패
          res.send({ status: "failed", message });
        }
      } catch (e) {
        res.status(400).send(e);
      }
    });
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="success" %}
**REST API 를 이용하기 위해서는** [**Access Token**](../../../api/rest-api-access-token.md) **획득이 선행되어야 하는점 잊지 마세요**
{% endhint %}

{% hint style="info" %}
**빌링키 발급과 결제 요청를 한번에 하기**

키인결제 REST API [**`/subscribe/payments/onetime`**](../../../api/api-4/)를 사용하면 빌링키 발급과 최초 결제를 같이 요청할 수 있습니다.
{% endhint %}

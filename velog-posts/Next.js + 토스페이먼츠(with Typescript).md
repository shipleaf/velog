<p>토스페이먼츠는 두 가지 방법으로 구현할 수 있고, 각 방법은 장단점을 가집니다.</p>
<ul>
<li>결제 위젯</li>
<li>결제 창<br />

</li>
</ul>
<p>이 포스트에서는 결제 위젯으로 구현을 진행했습니다.</p>
<p>결제 위젯:</p>
<p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/386d20ef-7cf7-481c-a95f-ade9fcfc3ba4/image.png" /></p>
<p>결제위젯에서의 결제 흐름은 다음과 같습니다.</p>
<ol>
<li>주문서 진입 및 결제위젯 렌더 요청</li>
</ol>
<p>코드는 토스페이먼츠 version2의 React+Java 코드를 Next.js에 맞게 변형하였습니다.</p>
<p>코드를 작성하기 전에 프로젝트에 결제위젯 sdk를 설치합니다.</p>
<pre><code class="language-js">npm install @tosspayments/tosspayments-sdk --save</code></pre>
<p>제가 진행중인 프로젝트는 아직 PG사가 확정되지 않아 개발자용 테스트키로 진행하였습니다.</p>
<p>1) 테스트 키</p>
<pre><code class="language-js">const clientKey = &quot;test_gck_docs_Ovk5rk1EwkEbP0W43n07xlzm&quot;;
const customerKey = generateRandomString();</code></pre>
<ul>
<li>clinetKey: 결제위젯 생성을 위한 파라미터로, 상점이나 제품을 식별하기 위한 key로 쓰입니다(문서에는 sdk 초기화로 표현되어 있습니다).</li>
<li>customerKey: 고객을 식별하기 위한 key입니다.</li>
</ul>
<p>2) 결제위젯 SDK 초기화</p>
<pre><code class="language-js">useEffect(() =&gt; {
    async function fetchPaymentWidgets() {
      try {
        // ------  SDK 초기화 ------
        // @docs https://docs.tosspayments.com/sdk/v2/js#토스페이먼츠-초기화
        const tossPayments = await loadTossPayments(clientKey);

        // 회원 결제
        // @docs https://docs.tosspayments.com/sdk/v2/js#tosspaymentswidgets
        const widgets = tossPayments.widgets({
          customerKey,
        });
        // 비회원 결제
        // const widgets = tossPayments.widgets({ customerKey: ANONYMOUS });

        setWidgets(widgets);
      } catch (error) {
        console.error(&quot;Error fetching payment widget:&quot;, error);
      }
    }

    fetchPaymentWidgets();
  }, [clientKey, customerKey]);</code></pre>
<p>저는 모듈 임포트 방식을 선택했기 때문에 loadTossPayments 함수를 사용합니다. 해당 함수는 clientKey를 파라미터로 하고, widgets, brandpay, payment등을 객체로 반환합니다.</p>
<p>loadTossPayments의 반환함수인 widgets()에 customerKey를 이용하여 위젯을 초기화합니다. 이렇게 초기화된 위젯을 useState로 선언해둔 widget으로 선언합니다.</p>
<p>3) 결제위젯 상세 설정</p>
<pre><code class="language-js">useEffect(() =&gt; {
    async function renderPaymentWidgets() {
      if (widgets == null) {
        return;
      }

      // ------  주문서의 결제 금액 설정 ------
      // TODO: 위젯의 결제금액을 결제하려는 금액으로 초기화하세요.
      // TODO: renderPaymentMethods, renderAgreement, requestPayment 보다 반드시 선행되어야 합니다.
      await widgets.setAmount(amount);

      // ------  결제 UI 렌더링 ------
      // @docs https://docs.tosspayments.com/sdk/v2/js#widgetsrenderpaymentmethods
      await widgets.renderPaymentMethods({
        selector: &quot;#payment-method&quot;,
        // 렌더링하고 싶은 결제 UI의 variantKey
        // 결제 수단 및 스타일이 다른 멀티 UI를 직접 만들고 싶다면 계약이 필요해요.
        // @docs https://docs.tosspayments.com/guides/v2/payment-widget/admin#새로운-결제-ui-추가하기
        variantKey: &quot;DEFAULT&quot;,
      });

      // ------  이용약관 UI 렌더링 ------
      // @docs https://docs.tosspayments.com/reference/widget-sdk#renderagreement선택자-옵션
      await widgets.renderAgreement({
        selector: &quot;#agreement&quot;,
        variantKey: &quot;AGREEMENT&quot;,
      });

      setReady(true);
    }

    renderPaymentWidgets();
  }, [widgets]);</code></pre>
<p>TossPaymentsWidgets 함수는 아래 객체를 반환합니다.</p>
<pre><code class="language-js">{
  setAmount: 결제 금액을 설정
  renderPaymentMethods: 결제 UI를 렌더링
  requestPayment: 결제 요청, 사용자가 선택한 결제 방식의 UI를 렌더링
  renderAgreement: 약관 UI 렌더링
}</code></pre>
<p>Typescript에서는 객체의 인터페이스를 작성해주어야 하는데, tosspayments-sdk에서 TossPaymentWidgets를 import해서 작성해주시면 됩니다.</p>
<p>4) 최종 코드</p>
<pre><code class="language-js">&quot;use client&quot;;

import {
  loadTossPayments,
  TossPaymentsWidgets,
} from &quot;@tosspayments/tosspayments-sdk&quot;;
import { useEffect, useState } from &quot;react&quot;;

function generateRandomString() {
  if (typeof window !== &quot;undefined&quot;) {
    return window.btoa(Math.random().toString()).slice(0, 20);
  }
  return &quot;&quot;; // 서버 환경일 경우 기본값 반환
}

// TODO: clientKey는 개발자센터의 결제위젯 연동 키 &gt; 클라이언트 키로 바꾸세요.
// TODO: 구매자의 고유 아이디를 불러와서 customerKey로 설정하세요. 이메일・전화번호와 같이 유추가 가능한 값은 안전하지 않습니다.
// @docs https://docs.tosspayments.com/sdk/v2/js#토스페이먼츠-초기화
const clientKey = &quot;test_gck_docs_Ovk5rk1EwkEbP0W43n07xlzm&quot;;
const customerKey = generateRandomString();

interface Amount {
  currency: string;
  value: number;
}

export default function CheckoutPage() {
  const [amount, setAmount] = useState&lt;Amount&gt;({
    currency: &quot;KRW&quot;,
    value: 50000,
  });
  const [ready, setReady] = useState(false);
  const [widgets, setWidgets] = useState&lt;TossPaymentsWidgets | null&gt;(null);

  useEffect(() =&gt; {
    async function fetchPaymentWidgets() {
      try {
        // ------  SDK 초기화 ------
        // @docs https://docs.tosspayments.com/sdk/v2/js#토스페이먼츠-초기화
        const tossPayments = await loadTossPayments(clientKey);

        // 회원 결제
        // @docs https://docs.tosspayments.com/sdk/v2/js#tosspaymentswidgets
        const widgets = tossPayments.widgets({
          customerKey,
        });
        // 비회원 결제
        // const widgets = tossPayments.widgets({ customerKey: ANONYMOUS });

        setWidgets(widgets);
      } catch (error) {
        console.error(&quot;Error fetching payment widget:&quot;, error);
      }
    }

    fetchPaymentWidgets();
    // eslint-disable-next-line
  }, [clientKey, customerKey]);

  useEffect(() =&gt; {
    async function renderPaymentWidgets() {
      if (widgets == null) {
        return;
      }

      // ------  주문서의 결제 금액 설정 ------
      // TODO: 위젯의 결제금액을 결제하려는 금액으로 초기화하세요.
      // TODO: renderPaymentMethods, renderAgreement, requestPayment 보다 반드시 선행되어야 합니다.
      await widgets.setAmount(amount);

      // ------  결제 UI 렌더링 ------
      // @docs https://docs.tosspayments.com/sdk/v2/js#widgetsrenderpaymentmethods
      await widgets.renderPaymentMethods({
        selector: &quot;#payment-method&quot;,
        // 렌더링하고 싶은 결제 UI의 variantKey
        // 결제 수단 및 스타일이 다른 멀티 UI를 직접 만들고 싶다면 계약이 필요해요.
        // @docs https://docs.tosspayments.com/guides/v2/payment-widget/admin#새로운-결제-ui-추가하기
        variantKey: &quot;DEFAULT&quot;,
      });

      // ------  이용약관 UI 렌더링 ------
      // @docs https://docs.tosspayments.com/reference/widget-sdk#renderagreement선택자-옵션
      await widgets.renderAgreement({
        selector: &quot;#agreement&quot;,
        variantKey: &quot;AGREEMENT&quot;,
      });

      setReady(true);
    }

    renderPaymentWidgets();
    // eslint-disable-next-line
  }, [widgets]);

  const updateAmount = async (amount: Amount) =&gt; {
    setAmount(amount);
    await widgets!.setAmount(amount);
  };

  return (
    &lt;div className=&quot;wrapper&quot;&gt;
      &lt;div className=&quot;box_section&quot;&gt;
        {/* 결제 UI */}
        &lt;div id=&quot;payment-method&quot; /&gt;
        {/* 이용약관 UI */}
        &lt;div id=&quot;agreement&quot; /&gt;
        {/* 쿠폰 체크박스 */}
        &lt;div style={{ paddingLeft: &quot;24px&quot; }}&gt;
          &lt;div className=&quot;checkable typography--p&quot;&gt;
            &lt;label
              htmlFor=&quot;coupon-box&quot;
              className=&quot;checkable__label typography--regular&quot;
            &gt;
              &lt;input
                id=&quot;coupon-box&quot;
                className=&quot;checkable__input&quot;
                type=&quot;checkbox&quot;
                aria-checked=&quot;true&quot;
                disabled={!ready}
                // ------  주문서의 결제 금액이 변경되었을 경우 결제 금액 업데이트 ------
                // @docs https://docs.tosspayments.com/sdk/v2/js#widgetssetamount
                onChange={async (event) =&gt; {
                  await updateAmount({
                    currency: amount.currency,
                    value: event.target.checked
                      ? amount.value - 5000
                      : amount.value + 5000,
                  });
                }}
              /&gt;
              &lt;span className=&quot;checkable__label-text&quot;&gt;5,000원 쿠폰 적용&lt;/span&gt;
            &lt;/label&gt;
          &lt;/div&gt;
        &lt;/div&gt;

        {/* 결제하기 버튼 */}
        &lt;button
          className=&quot;button&quot;
          style={{ marginTop: &quot;30px&quot; }}
          disabled={!ready}
          // ------ '결제하기' 버튼 누르면 결제창 띄우기 ------
          // @docs https://docs.tosspayments.com/sdk/v2/js#widgetsrequestpayment
          onClick={async () =&gt; {
            try {
              // 결제를 요청하기 전에 orderId, amount를 서버에 저장하세요.
              // 결제 과정에서 악의적으로 결제 금액이 바뀌는 것을 확인하는 용도입니다.
              await widgets!.requestPayment({
                orderId: generateRandomString(),
                orderName: &quot;토스 티셔츠 외 2건&quot;,
                successUrl: window.location.origin + &quot;/success&quot;,
                failUrl: window.location.origin + &quot;/fail&quot;,
                customerEmail: &quot;customer123@gmail.com&quot;,
                customerName: &quot;김토스&quot;,
                customerMobilePhone: &quot;01012341234&quot;,
              });
            } catch (error) {
              // 에러 처리하기
              console.error(error);
            }
          }}
        &gt;
          결제하기
        &lt;/button&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
}</code></pre>
<ol start="2">
<li>SuccessURL 이동 및 결제 승인</li>
</ol>
<p>이후, SuccessURL 이동 및 결제 완료 페이지인 success.tsx와 fail.tsx는 크게 달리지는 점이 없습니다. 다만, 각 페이지에서 사용되는 이미지의 최적화를 위해 next.config.ts에 toss.im을 추가해줍니다.</p>
<pre><code class="language-js">import type { NextConfig } from &quot;next&quot;;

const nextConfig: NextConfig = {
  images: {
    domains: ['static.toss.im'], // 허용할 이미지 호스트 도메인 추가
  },
};

export default nextConfig;
</code></pre>
<br />
<br />

<h4 id="문서">문서</h4>
<hr />
[토스페이먼츠 문서보기](https://docs.tosspayments.com/guides/v2/payment-widget/integration?frontend=react&amp;backend=java)
[https://github.com/shipleaf/PG_Tosspayments_Study](https://github.com/shipleaf/PG_Tosspayments_Study)
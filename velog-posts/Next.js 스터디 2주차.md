<h2 id="1-csrssrssg-이해하기">1. CSR/SSR/SSG 이해하기</h2>
<p>CSR/SSR/SSG는 페이지 렌더링 방식으로 TTFB, FCP등의 정량적 지표로 성능을 비교할 수는 있지만 상황과 설계에 따라 값이 달라질 수 있어 의미가 크지는 않다. 따라서 정성적으로 비교를 해본다. </p>
<h3 id="1-ssr">1. SSR</h3>
<p>블로그, 홈페이지 웹사이트 등 php나 Java의 서버 사이트 템플릿 엔진을 이용해서 개발된다.</p>
<p>SSR은 페이지를 바꿀때 새로운 Html 문서가 나온다. 즉, 완성된 Html이 서버에서 만들어진 뒤 브라우저에 전송되고 브라우저는 해당 Html을 바로 렌더링하는 방식이다. 따라서, 초기 용량이 작고 보안에 유리하다. 또한, 완성된 Html이 크롤링을 하기 좋은 환경이기 때문에 SEO에 좋다.</p>
<p>하지만, 페이지마다 새로운 Html을 그려줘야 하기 때문에 페이지 라우팅시 화면 깜빡임이 있을 수 있고, 사용자가 많아지면 서버에 부하가 증가한다.</p>
<h4 id="장점">장점</h4>
<ul>
<li>초기 용량이 작다</li>
<li>보안에 유리하다</li>
<li>SEO에 좋다<h4 id="단점">단점</h4>
</li>
<li>페이지 라우팅시 화면 깜빡임이 있을 수 있다</li>
<li>사용자 수가 많아지면 서버 부하가 증가한다</li>
</ul>
<h3 id="2-csr">2. CSR</h3>
<p>CRA(create-react-app)로 만든 react 앱이 CSR 방식으로 웹을 렌더링한다. CSR방식은 SSR과 다르게 html 문서에 root id를 가진 div 외엔 아무것도 없다. 나머지 DOM을 자바스크립트로 렌더링하는 방식을 사용한다.</p>
<p>CSR 방식은 초기에 적은 Html만 받고 나머지는 자바스크립트로 그리기 때문에 화면 깜빡임이 없다. 하지만, CSR 방식은 자바스크립트 파일(라이브러리, 프레임워크 등)을 서버로부터 다운받아 화면에 렌더링하기 때문에 초기 용량이 크다. 또한, 서버에서 렌더링하는 것이 아닌 자바스크립트로 렌더링하기 때문에 캐시는 가능하지만, 보안에는 취약하다. SSR에 비해 SEO에도 제약이 있다.</p>
<h4 id="장점-1">장점</h4>
<ul>
<li>화면 깜빡임이 없다</li>
<li>캐시가 가능하다<h4 id="단점-1">단점</h4>
</li>
<li>초기 용량이 크다</li>
<li>보안에 취약하다</li>
<li>SEO에 제약이 있다</li>
</ul>
<h3 id="3-ssg">3. SSG</h3>
<p>SSG방식은 pre-rendering 개념 차용, 정적인 Html을 build time에 미리 만들어둔다. 사이트에 접속할 때마다 Html 문서를 만든다. 따라서, 내용이 동적으로 변하지 않는 정적인 사이트에 이용한다. 브라우저 관리자 도구를 통해 캐시를 꺼두어도 Html 문서에 캐시가 포함되어 있어 캐시된 Html 문서를 똑같이 받을 수 있다.</p>
<h4 id="장점-2">장점:</h4>
<ul>
<li>서버에 부하가 없다</li>
<li>Html 문서 자체를 캐시할 수 있다</li>
<li>SEO에 좋다</li>
</ul>
<h2 id="2-nextjs를-사용하는-이유">2. Next.js를 사용하는 이유</h2>
<p>Next.js는 SSR, CSR, SSG의 장점(작은 용량과 보안, 빠른 페이지 이동속도 및 깜빡임 없음)만 고려하여 페이지를 자유롭게 렌더링, 라우팅할 수 있도록 API를 제공한다. 현존하는 기술들의 장점을 모아 새로운 기능을 개발하는 것이 Next.js의 방향성이다.</p>
<p>React와 Next.js의 가장 큰 차이점은 Pre-rendering의 유무이다. Pre-rendering이란, 쉽게 말해 Html 문서를 미리 만들어두는 것이다.</p>
<ul>
<li><p>CRA(Pre-rendering 지원안함)
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/937efc5a-a1df-4fcc-927f-370574f629f8/image.gif" />
React로 만들어진 토스 웹사이트를 자바스크립트 삭제 했을때 컨텐츠의 내용이 사라진다.</p>
</li>
<li><p>Next.js(Pre-rendering 지원함)
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/56f3a759-d521-4c7d-8540-db55ad9475ea/image.gif" />
Next.js로 만든 웹사이트는 자바스크립트를 삭제해도 문제없이 사용할 수 있다.</p>
</li>
</ul>
<h2 id="3-getstaticprops">3. getStaticProps</h2>
<pre><code>import type { NextPage } from 'next';

interface Props {
  data: number;
}

const Example: NextPage&lt;Props&gt; = ({ data }) =&gt; {
  return (
    &lt;main&gt;
      &lt;h1&gt;getStaticProps Page&lt;/h1&gt;    // getStaticProps Page 문자열 화면에 출력한다.
      &lt;p&gt;값: {data}&lt;/p&gt;    // data를 parameter로 받아와 출력한다.
    &lt;/main&gt;
  );
};

export default Example;

// 데이터는 next.js의 getStaticProps 함수에서 불러온다.

export async function getStaticProps() {
  const delayInSeconds = 2;    //magic number 설정
  const data = await new Promise((resolve) =&gt;
    setTimeout(() =&gt; resolve(Math.random()), delayInSeconds * 1000)
  );    // 0 ~ 1 사이의 랜덤한 수를 받아온다.

  return {
    props: { data }
}</code></pre><p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/028ccede-2ddb-48d1-a224-5ab8c0fc666d/image.gif" /></p>
<p>코드를 실행하면 개발자 도구의 preview 탭에서 Html 문서가 pre-rendering됨을 확인할 수 있다. </p>
<p>하지만, 우리가 원하는 SSG 방식은 값이 정적으로 변하지 않아야 한다. getStaticProps 함수를 사용했음에도 값이 변하는 이유는 개발 환경에서 코드를 실행했기 때문이다. 개발 환경에서는 새로고침시 getStaticProps 함수를 실행하도록 설정되어있다.</p>
<p>Production(실제 서비스) 환경에서 코드를 실행하려면</p>
<pre><code>yarn build
yarn start</code></pre><p>위 코드를 이용한다.</p>
<p>production 환경에서 코드를 실행하면 값이 정적으로 바뀌지 않고 새로고침해도 같은 값으로 출력된다.</p>
<p>값의 변경이 있는 웹에서 이를 반영하려면 ISR의 revalidate를 이용한다</p>
<pre><code>revalidate: 5</code></pre><p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/1577f2af-0b5f-4972-975a-8b6056fe59b9/image.gif" /></p>
<p>위처럼 5초간 cache를 hit로 유지하고 2초간 stale로 변경 후 값을 다시 가져온다. 새로운 값을 받았을때 새로운 값으로 다시 pre-rendering을 하는 것이다.</p>
<p>만약 값이 고정되어 변하지 않는다면, next는 쓸모없는 pre-rendering을 수행하지 않는다.</p>
<h2 id="4-nextlink로-routing하기">4. next/link로 routing하기</h2>
<p>next/link로 페이지에서 다른 페이지로 라우팅을 할 수 있다.</p>
<pre><code>import Link from 'next/link';

export default function Links() {
  return (
    &lt;main&gt;
      &lt;h1&gt;Links&lt;/h1&gt;

      &lt;Link href=&quot;/section1/getStaticProps&quot;&gt;/getStaticProps&lt;/Link&gt;
    &lt;/main&gt;
  );
}</code></pre><p>위 코드의 link 태그가 a태그의 역할을 수행해 link를 생성하고 웹페이지가 처음 불러올때 기존 페이지의 Html문서와 이후 페이지의 js 파일을 불러온다. 기존 페이지에서 다음 페이지로 넘어갈때 js 코드를 CSR 방식으로 렌더링한다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/47843a87-6c28-400e-b805-2551520bd362/image.png" />
사진처럼 getStaticProps 파일이 다운받아진다.</p>
<p>link 태그는 link가 사용자에게 노출되기 전까지는 js 코드를 받지 않아 불필요한 네트워크 요청을 지양한다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/a402266e-b7db-4ce7-88c3-35808e61b02a/image.gif" /></p>
<h2 id="5-nextrouter로-routing하기">5. next/router로 routing하기</h2>
<p>next/router의 router.push 함수를 이용해서 button을 클릭했을때 페이지를 CSR로 렌더링할 수 있다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/685e1b1f-e5c3-4747-9f99-d1832caa6a88/image.gif" />
하지만, 이 방법은 버튼이 노출되기 전에도 js 코드를 다운받기 때문에 불필요한 네트워크 요청이 있을 수 있어 특별한 경우가 아니라면 next/link를 사용한다.</p>
<h2 id="6-next-폴더-확인하기">6. .next 폴더 확인하기</h2>
<p>Production 환경에서 코드를 실행시 위 예시의 getStaticProps Html 파일과 js는 어디에 저장될까?</p>
<p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/8e7f7fba-c34e-4f4f-9187-7d06748951dc/image.png" />
.next 폴더의 static/chunks/pages/section1 폴더에 저장된다. 위 js 파일의 hash 값은 서버에서 받은 js 파일의 hash 값과 동일하다.</p>
<h2 id="7-getserversideprops">7. getServerSideProps</h2>
<pre><code class="language-import">
interface Props {
  data: number;
}

const Example: NextPage&lt;Props&gt; = ({ data }) =&gt; {
  return (
    &lt;main&gt;
      &lt;h1&gt;getServerSideProps Page&lt;/h1&gt;
      &lt;p&gt;값: {data}&lt;/p&gt;
    &lt;/main&gt;
  );
};

export default Example;

export const getServerSideProps: GetServerSideProps = async ({ res }) =&gt; {

  const delayInSeconds = 2;
  const data = await new Promise((resolve) =&gt;
    setTimeout(() =&gt; resolve(Math.random()), delayInSeconds * 1000)
  );

  return {
    props: { data },
  };
};</code></pre>
<p>getStaticProps 코드와 유사하게 SSR 방식으로 렌더링하는 코드를 짜준다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/6b513520-7460-4c0c-a71c-6d3756742fed/image.gif" />
getServerSideProps는 SSG 방식과 달리 페이지를 새로고침 할때마다 페이지가 pending 된다. 즉, 페이지의 build time이 아닌, request time에 맞춰 렌더링된다. 때문에 SSG에 비해 사용자 경험이 좋지 않다.</p>
<p>페이지가 동적으로 변하지만 보안은 중요한 웹 사이트에서 위의 방식을 채용한다.</p>
<h2 id="8-csr">8. CSR</h2>
<pre><code>import type { NextPage } from 'next';
import { useEffect, useState } from 'react';
import dynamic from 'next/dynamic';

const Example: NextPage = () =&gt; {
  const [data, setData] = useState(0);

  useEffect(() =&gt; {
    const delayInSeconds = 2;
    new Promise&lt;number&gt;((resolve) =&gt;
      setTimeout(() =&gt; resolve(Math.random()), delayInSeconds * 1000)
    ).then((result) =&gt; setData(result));
  }, []);    값을 바꾸는 메인로직 설정

  return (
    &lt;main&gt;
      &lt;h1&gt;Client-side data fetching&lt;/h1&gt;
      &lt;p&gt;값: {data}&lt;/p&gt;

    &lt;/main&gt;
  );
};

export default Example;
</code></pre><p>위 코드는 next에서 CSR 방식을 사용하는 코드이다 실행해보면 2초뒤에 값이 찍힌다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/907ac019-7fa4-498e-afda-1b953fa847ac/image.png" />
SSG와 SSR 방법과는 다르게 client에서 렌더링을 하기 때문에 미리보기 창에는 값이 출력되지 않는다(초기 상태인 0으로 pre-rendering 함).</p>
<pre><code>const NoSSR = () =&gt; {
    return &lt;p&gt;width: {window.innerWidth}&lt;/p&gt;;    // window.innerWidth를 렌더링하는 코드
};

  export default NoSSR;
</code></pre><p>위 코드를 import 해서 실행했을때</p>
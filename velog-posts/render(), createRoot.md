<h3 id="에러-발생">에러 발생</h3>
<p>JSX 코드</p>
<pre><code>import React from &quot;react&quot;;

function Clock(props) {
    return (
        &lt;div&gt;
            &lt;h1&gt;안녕, 리엑트!&lt;/h1&gt;
            &lt;h2&gt;현재 시간: {new Date().toLocaleTimeString()}&lt;/h2&gt;
        &lt;/div&gt;
    );
}

export default Clock;</code></pre><p>Html 코드</p>
<pre><code>import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

import Clock from './ch_04/Clock';

setInterval(() =&gt; {
  ReactDOM.render(
    &lt;React.StrictMode&gt;
      &lt;Clock /&gt;
    &lt;/React.StrictMode&gt;,
    document.getElementById('root')
  )
}, 1000);

reportWebVitals();
</code></pre><p>위 코드들로 Clock component를 만들고 렌더링하는 과정에서 아래의 
Uncaught runtime errors: react_dom_client__WEBPACK_IMPORTED_MODULE_1__render is not a function가 발생했다. 
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/af1d7623-e02c-4c7c-a315-14b6c0b9ff5a/image.gif" /></p>
<p>찾아보니 react v18 부터는 ReactDOM API의 render 함수를 지원하지 않는다고 한다. 대신 createRoot를 이용한다.</p>
<pre><code>// React17
import React from &quot;react&quot;;
import ReactDOM from &quot;react-dom&quot;;
import App from &quot;./App&quot;;

ReactDOM.render(&lt;Clock /&gt;, document.getElementById(&quot;root&quot;));

// React18
import React from &quot;react&quot;;
import App from &quot;./App&quot;;
import { createRoot } from &quot;react-dom/client&quot;;

const container = document.getElementById(&quot;root&quot;);
root.render(&lt;Clock/&gt;);</code></pre><p>React-DOM의 render()함수와 createRoot의 차이는 createRoot가 동시성 API와 Automatic Batching을 지원한다는 것이다. </p>
<ul>
<li>동시성:
긴급 업데이트: 타이핑등의 직접적인 상호 작용을 반영해야 한다. 사용자의 입력(타이핑 등)에 따라 즉각적으로 업데이트되지 않으면 문제가 있다고 느끼는 영역이다.
전환 업데이트: 하나의 화면에서 다른 화면으로의 전환, 화면에 바로 나타나는 걸 기대하지 않는 영역이다.</li>
</ul>
<p>React 17v 까지는 긴급, 전환 업데이트의 경계가 분명하지 않아, 전환 업데이트가 긴급 업데이트를 방해하는 경우가 있었다. 18v 부터는 명시가 가능해지고, 방해하지 않는다.</p>
<ul>
<li>Batching: 리액트가 더 나은 성능을 위해 여러개의 state업데이트를  re-render를 최소화하도록 그룹화 하는 것을 의미한다. Automatic Batching을 이용해 작업 렌더링을 최소화하고 성능 향상을 기대할 수 있다. </li>
</ul>
<h3 id="에러-해결">에러 해결</h3>
<pre><code>import React from &quot;react&quot;;
import &quot;./index.css&quot;;
import reportWebVitals from &quot;./reportWebVitals&quot;;
import { createRoot } from &quot;react-dom/client&quot;;
import Clock from &quot;./chapter_04/clock&quot;;

const root = createRoot(document.getElementById(&quot;root&quot;));

setInterval(() =&gt; {
  root.render(
    &lt;React.StrictMode&gt;
      &lt;Clock /&gt;
    &lt;/React.StrictMode&gt;
  );
}, 1000);

reportWebVitals();</code></pre><p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/5e8e9b2b-42b2-4b05-8ebb-e22cd17ca430/image.gif" />
위와 같이 결과가 잘 나온다.</p>
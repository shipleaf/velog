<h2 id="react-상태관리">React 상태관리</h2>
<p>React 주요 상태관리 라이브러리 다운로드 수</p>
<p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/f0eb9fe5-015a-47ed-81bc-1c8e886656b4/image.png" />
(npm trends)</p>
<h3 id="1-recoil">1. Recoil</h3>
<ul>
<li>React의 State와 유사한 API 제공</li>
<li>컴포넌트별로 구독을 지원</li>
<li>기본적으로 동기적으로 작동, selector를 이용해 비동기로 구현 가능</li>
</ul>
<pre><code>// atom.js

import { atom } from 'recoil';

export const counterState = atom({
  key: 'counterState',    // 키 값
  default: 0,    // default 값
});</code></pre><pre><code>import React from 'react';
import { useRecoilState } from 'recoil';
import { counterState } from './atoms';

function Counter() {
  const [count, setCount] = useRecoilState(counterState);

  const increment = () =&gt; setCount(count + 1);
  const decrement = () =&gt; setCount(count - 1);

  return (
    &lt;div&gt;
      &lt;h2&gt;Count: {count}&lt;/h2&gt;
      &lt;button onClick={increment}&gt;+&lt;/button&gt;
      &lt;button onClick={decrement}&gt;-&lt;/button&gt;
    &lt;/div&gt;
  );
}

export default Counter;</code></pre><h3 id="2-redux">2. Redux</h3>
<ul>
<li>전역 상태 관리를 위한 가장 유명한 라이브러리</li>
<li>중앙 집중식 상태 저장소와 액션, 리듀서를 통해 상태 변경을 제어</li>
<li>대규모 어플리케이션에서 주로 사용되며, 비동기 작업을 처리하기 위해 Redux-Saga, Redux-Thunk 같은 미들웨어와 함께 사용</li>
</ul>
<pre><code>/// store.js

import { configureStore } from '@reduxjs/toolkit';
import counterReducer from './counterSlice';

const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});

export default store;</code></pre><pre><code>import { createSlice } from '@reduxjs/toolkit';

export const counterSlice = createSlice({
  name: 'counter',
  initialState: {
    value: 0,
  },
  reducers: {
    increment: (state) =&gt; {
      state.value += 1;
    },
    decrement: (state) =&gt; {
      state.value -= 1;
    },
    incrementByAmount: (state, action) =&gt; {
      state.value += action.payload;
    },
  },
});

export const { increment, decrement, incrementByAmount } = counterSlice.actions;

export default counterSlice.reducer;
</code></pre><pre><code>import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { increment, decrement, incrementByAmount } from './counterSlice';

function Counter() {
  const count = useSelector((state) =&gt; state.counter.value);
  const dispatch = useDispatch();

  return (
    &lt;div&gt;
      &lt;h2&gt;Count: {count}&lt;/h2&gt;
      &lt;button onClick={() =&gt; dispatch(increment())}&gt;+&lt;/button&gt;
      &lt;button onClick={() =&gt; dispatch(decrement())}&gt;-&lt;/button&gt;
      &lt;button onClick={() =&gt; dispatch(incrementByAmount(5))}&gt;+5&lt;/button&gt;
    &lt;/div&gt;
  );
}

export default Counter;
</code></pre><h3 id="3-zustand">3. zustand</h3>
<ul>
<li>경량 상태 관리 라이브러리로, 간단한 API로 전역 상태를 관리</li>
<li>전역 상태를 간편하게 사용할 수 있어 소규모 프로젝트에 적합<pre><code>import create from 'zustand';
</code></pre></li>
</ul>
<p>const useStore = create((set) =&gt; ({
  count: 0,                    // 초기 상태
  increase: () =&gt; set((state) =&gt; ({ count: state.count + 1 })), // 증가
  decrease: () =&gt; set((state) =&gt; ({ count: state.count - 1 })), // 감소
}));</p>
<pre><code></code></pre><p>import React from 'react';
import useStore from './store';</p>
<p>function Counter() {
  const { count, increase, decrease } = useStore();</p>
<p>  return (
    <div>
      <h2>Count: {count}</h2>
      <button>Increase</button>
      <button>Decrease</button>
    </div>
  );
}</p>
<p>export default Counter;</p>
<p>```</p>
<h3 id="각-라이브러리-장단점">각 라이브러리 장단점</h3>
<blockquote>
<h3 id="recoil">Recoil:</h3>
</blockquote>
<ul>
<li>장점</li>
</ul>
<ol>
<li>React 전용으로 설계되어 사용법이 useState와 유사해 배우기 쉽고, React와의 호환성이 높다.</li>
</ol>
<ul>
<li>단점</li>
</ul>
<ol>
<li>상대적으로 작은 생태계: Redux만큼 성숙한 미들웨어나 플러그인이 부족하다.</li>
<li>대규모 프로젝트에서의 제한적: 아직 대규모 애플리케이션에서의 최적화와 패턴에 대한 확립이 부족한 편이다.</li>
</ol>
<blockquote>
<h3 id="redux">Redux</h3>
</blockquote>
<ul>
<li>장점</li>
</ul>
<ol>
<li>성숙한 생태계: Redux는 오랜 시간 동안 사용된만큼 다양한 미들웨어와 플러그인을 갖춘 커뮤니티가 형성되어 있다(redux-thunk, redux-saga 등의 미들웨어를 통해 복잡한 비동기 로직을 처리할 수 있음).</li>
<li>예측 가능한 상태 관리: 불변성을 유지하면서 상태를 변경하는 순수 함수 기반 리듀서로 예측 가능하고, 디버깅이 쉽다.</li>
<li>강력한 개발 도구: Redux DevTools를 통해 상태 변화와 액션을 추적할 수 있어 디버깅과 상태 관리가 용이하다.</li>
<li>타입스크립트와의 뛰어난 호환성: Redux Toolkit 덕분에 타입스크립트와의 호환성이 강화되어 타입 안전성을 유지하며 상태 관리가 가능하다.</li>
</ol>
<ul>
<li>단점</li>
</ul>
<ol>
<li>복잡한 코드: 리듀서, 액션, 스토어 설정 등 추가적인 코드가 많이 필요하여 코드가 길어지고 복잡해질 수 있습니다.</li>
<li>소규모 프로젝트에는 과함: 복잡한 상태 관리가 필요하지 않은 경우에는 설정이 지나치게 복잡할 수 있다.</li>
</ol>
<blockquote>
<h3 id="zustand">Zustand</h3>
</blockquote>
<ul>
<li>장점</li>
</ul>
<ol>
<li>간단한 설정과 사용법: create 함수 하나로 상태를 정의할 수 있어, 별도의 템플릿 코드 없이 빠르게 전역 상태 관리를 설정한다.</li>
<li>구독 기반 상태 관리: 필요한 상태만 구독하고 업데이트하므로 불필요한 리렌더링을 줄여 성능을 최적화 가능하다.</li>
<li>비동기 데이터 처리의 용이성: 비동기 상태를 별도의 설정 없이 함수로 간단히 정의할 수 있다.</li>
<li>다양한 규모의 프로젝트에 유연함: 작은 코드 베이스로 소규모 프로젝트에서 효과적이고, slice 단위로 나누어 대규모 프로젝트에서도 유연하게 관리할 수 있다.</li>
</ol>
<ul>
<li>단점</li>
</ul>
<ol>
<li>미들웨어 및 생태계 부족: Recoil이나 Redux만큼 다양한 미들웨어와 커뮤니티 지원이 부족하다.</li>
<li>대규모 상태 관리에 약함: 상태의 구조화와 의존성 관리가 부족해 복잡한 상태와 의존성을 다루는 대규모 프로젝트에서는 제한적일 수 있다.</li>
<li>디버깅 도구의 부족: 상태 추적과 디버깅을 지원하는 DevTools가 부족해, 대규모 프로젝트에서 상태 변화 추적이 어렵다.</li>
</ol>
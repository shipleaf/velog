<h2 id="redux">Redux</h2>
<p>전역 상태 관리를 위한 가장 유명한 라이브러리
중앙 집중식 상태 저장소와 액션, 리듀서를 통해 상태 변경을 제어
대규모 어플리케이션에서 주로 사용되며, 비동기 작업을 처리하기 위해 Redux-Saga, Redux-Thunk 같은 미들웨어와 함께 사용</p>
<h3 id="1-액션">1. 액션</h3>
<pre><code>/actions/counterActions.js

export const increment = () =&gt; {
    return {
        type: 'INCREMENT'
    };
};

export const decrement = () =&gt; {
    return {
        type: 'DECREMENT'
    };
};</code></pre><blockquote>
<p>type은 객체, 액션은 전역 상태 관리에 사용할 함수의 타입을 지정하는 것!(이름)</p>
</blockquote>
<h3 id="2-reducer">2. Reducer</h3>
<pre><code>/reducers/counterReducer.js

const initialState = {
    count: 0
};

const counterReducer = (state = initialState, action) =&gt; {
    switch (action.type) {    // switch 문 사용
        case 'INCREMENT':
            return {
                ...state,
                count: state.count + 1
            };
        case 'DECREMENT':
            return {
                ...state,
                count: state.count - 1
            };
        default:
            return state;
    }
};

export default counterReducer;</code></pre><blockquote>
<p>initialState는 전역 변수의 default 값을 의미, Reducer는 변수의 초기 값과 각 action이 변수를 어떻게 변하게 하는지 정의하는 곳!</p>
</blockquote>
<h3 id="3-store">3. store</h3>
<pre><code>/store.js
import { createStore } from 'redux';
import counterReducer from './reducers/counterReducer';

const store = createStore(counterReducer);

export default store;</code></pre><blockquote>
<p>store는 전역 변수들을 한번에 관리하는 곳, 변수가 여러개라면?</p>
</blockquote>
<pre><code>/reducers/index.js
import { combineReducers } from 'redux';
import counterReducer from './counterReducer';
import userReducer from './userReducer';

const rootReducer = combineReducers({
    counter: counterReducer,
    user: userReducer    // 새로운 전역변수
});

export default rootReducer;</code></pre><blockquote>
<p>combineReducers 함수를 통해 rootReducer를 생성</p>
</blockquote>
<pre><code>/store.js
import { createStore } from 'redux';
import rootReducer from './reducers';

const store = createStore(rootReducer);

export default store;
</code></pre><blockquote>
<p>store에 rootReducer를 이용해 store를 선언해주면 된다</p>
</blockquote>
<h3 id="4-provider">4. Provider</h3>
<pre><code>/index.js
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import store from './store';
import App from './App';

ReactDOM.render(
    &lt;Provider store={store}&gt;
        &lt;App /&gt;
    &lt;/Provider&gt;,
    document.getElementById('root')
);
</code></pre><blockquote>
<p>store에 있는 전역변수들을 사용하기 위해서는 최상위 컴포넌트를 Provider 태그로 감싸야 한다.</p>
</blockquote>
<h3 id="5-사용예시">5. 사용예시</h3>
<pre><code>/components/Counter.js
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { increment, decrement } from '../actions/counterActions';

const Counter = () =&gt; {
    const count = useSelector((state) =&gt; state.count);
    const dispatch = useDispatch();

    return (
        &lt;div&gt;
            &lt;h1&gt;Count: {count}&lt;/h1&gt;
            &lt;button onClick={() =&gt; dispatch(increment())}&gt;+&lt;/button&gt;
            &lt;button onClick={() =&gt; dispatch(decrement())}&gt;-&lt;/button&gt;
        &lt;/div&gt;
    );
};

export default Counter;</code></pre><blockquote>
<p>useSelector를 사용해 전역변수를 불러오고, useDispatch를 통해 선언해둔 액션을 추적, 실행할 수 있다.</p>
</blockquote>
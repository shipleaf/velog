<h2 id="reacy-query-알아보기">Reacy Query 알아보기</h2>
<hr /><br />
최근 많은 기업들이 기존의 Fetch API + 전역 변수 관리 라이브러리(Redux, MobX 등...)에서 React Query + 클라이언트의 상태를 관리하는 비교적 간단한 라이브러리(Recoil, Zustand 등..)로 방식을 변경하고 있습니다. 이에 두 방식을 비교해보고 React Query를 왜 사용하는지에 대해 기술해보고자 합니다.<br /><br />

<hr />
<br />

<h3 id="목차">목차</h3>
<ol>
<li>왜 React Query인가?</li>
<li>React Query 문법</li>
<li>기존 방식과 React Query의 비교</li>
<li>프로젝트 적용에 대한 고민</li>
<li>마무리</li>
</ol>
<br />
<hr />
<br />


<h3 id="1-왜-react-query인가">1. 왜 React Query인가?</h3>
<p>React Query를 공부해보기 전에 많은 블로그, 문서 등에서 React Query를 상태관리 라이브러리라고 하여 전역 변수 라이브러리와 혼동이 왔었습니다. React Query는 서버 데이터 관리 및 동기화를 도와주는 라이브러리로, 최근 많은 개발자 및 기업에서 적극 활용하는 추세입니다.</p>
<p>1) 데이터 Fetching 간소화</p>
<p>서버에서 데이터를 가져오는 작업을 간소화 시킬 수 있습니다.</p>
<p>2) 서버 상태 관리</p>
<p>React Query는 클라이언트 단에서 서버 데이터가 최신 상태를 유지하도록 합니다. 변화가 감지되면, 자동으로 데이터를 새로 가져옵니다.</p>
<p>3) 자동 Re-Fetch</p>
<p>컴포넌트가 다시 마운트되거나, 네트워크 연결이 복구되거나, 데이터가 오래되었을 때 서버에서 데이터를 가져옵니다. 따라서, ussEffect로 구현해야하는 불편함을 없애줍니다.</p>
<p>4) 데이터 캐싱 지원</p>
<p>React Query는 데이터 캐싱을 자체적으로 지원합니다. 사용자가 설정한 데이터에 대해 브라우저 메모리에 저장하고 사용하며, 데이터가 오래됐다고 판단시 삭제하고 새로 요청합니다.</p>
<p>데이터 캐싱은 useQuery 훅을 사용해 데이터를 가져오면 자동으로 캐싱되며, 캐싱 시간과 조건등은 사용자가 설정할 수 있습니다.</p>
<pre><code>cacheTime: 캐시를 얼마나 오래 유지할지 설정
staleTime: 데이터가 신선한 상태로 간주되는 시간 설정
refetchOnWindowFocus: 사용자가 창을 다시 활성화할 때 데이터를 새로 가져올지 여부 설정
enabled: 쿼리문을 동작하지 않도록 함</code></pre><p>캐싱은 useQuery의 기본 동작이므로 실행되지 않도록 설정할 수는 없지만 cacheTime이나 staleTime등을 설정하여 삭제될 수 있습니다.</p>
<p>필요에 따라 캐싱된 데이터를 영구 보관 장소(세션, 로컬 스토리지)에 보관할 수도 있습니다.</p>
<p>5) 간편한 설정</p>
<p>React Query는 간단한 사용법으로 러닝커브가 낮고, 필수 보일러플레이트가 적어 사용하기 쉽습니다. 또한, 최상위 컴포넌트를 QueryClientProvider 태그로 감싸면 사용 준비가 됩니다.</p>
<br />
<hr />
<br />

<h3 id="2-react-query-문법">2. React Query 문법</h3>
<ul>
<li><p>Query</p>
<pre><code class="language-js">const { data } = useQuery(
  queryKey,
  queryFunction,
  options,
)</code></pre>
<p>React Query에서는 기존에 GET으로 받아오는 대부분의 API에서 useQuery 훅을 사용합니다. useQuery는 총 세가지의 인자를 받습니다.</p>
</li>
<li><p>queryKey: 응답 데이터의 Key 값으로, 응답 데이터를 캐싱할 때 사용합니다.</p>
</li>
<li><p>queryFunction: 해당 쿼리를 요청하기 위한 fetch, axios 등의 함수를 넣습니다.</p>
</li>
<li><p>options: useQuery를 세부적으로 제어할 수 있는 객체</p>
</li>
</ul>
<p>options 예시)</p>
<pre><code class="language-js">useQuery(['todos', userId], fetchUserTodos, {
  enabled: userId !== null, // userId가 null일 때 비활성화
  staleTime: 1000 * 60 * 5, // 5분 동안 데이터 갱신 안 함
  cacheTime: 1000 * 60 * 10, // 10분 동안 캐시 유지
  onSuccess: (data) =&gt; console.log('Fetched data:', data),
  onError: (error) =&gt; console.error('Error fetching data:', error),
});</code></pre>
<p>useQuery 사용 예시)</p>
<pre><code class="language-js">import React from 'react';
import { useQuery } from 'react-query';

const fetchData = async () =&gt; {
  const response = await fetch('https://api.example.com/data');
  if (!response.ok) {
    throw new Error('Network response was not ok');
  }
  return response.json();
};

function ReactQueryExample() {
  const { data, isLoading, error } = useQuery('data', fetchData);

  if (isLoading) return &lt;div&gt;Loading...&lt;/div&gt;;
  if (error) return &lt;div&gt;Error: {error.message}&lt;/div&gt;;
  return &lt;div&gt;Data: {JSON.stringify(data)}&lt;/div&gt;;
}</code></pre>
<p>React Query의 일반적인 예시를 보기 위해 GPT의 도움을 이용했다. 기존과 비슷한 방식으로 fetchData를 정의한 후 컴포넌트 혹은 페이지에서 useQuery 훅을 이용하여 데이터를 간단하게 가져올 수 있다. </p>
<br />

<ul>
<li>Mutation<pre><code class="language-js">const mutation = useMutation(mutationFn, options);</code></pre>
mutation는 PUT, UPDATE, POST 요청을 처리하는 함수로, 요청 함수와 옵션을 인자로 받습니다.</li>
</ul>
<p>Options 예시)</p>
<pre><code class="language-js">onMutate: 변경 작업 시작 작전 실행, 낙관적 업데이트를 구현할 때 사용
onSuccess: 요청 성공 시 실행
onError: 요청 실패 시 실행
onSettled: 요청 성공 또는 실패 후 무조건 실행
retry: 요청 실패 시 재시도 횟수 설정(기본값: 3)
retryDelay: 재시도 간격</code></pre>
<br />
useMutation 사용 예시)

<pre><code>const addTodo = async (newTodo) =&gt; {
  const res = await fetch('/api/todos', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(newTodo),
  });
  return res.json();
};

const { mutate, isLoading, isError, error } = useMutation(addTodo);

const handleAddTodo = () =&gt; {
  mutate({ title: 'New Todo' });
};</code></pre><p>위 코드의 handleAddTodo 함수에서 mutate라는 함수를 사용하고 있다. useMutation은 실행시 객체를 반환하며, mutate도 해당 객체 중 하나로, 요청을 트리거하는 함수이다. </p>
<br />
<hr />
<br />

<h3 id="3-기존-방식과-react-query의-비교">3. 기존 방식과 React Query의 비교</h3>
<p>위 코드를 보면 알 수 있듯, useQuery와 useMutataion 함수는 에러, 로딩 등의 상태를 자동으로 처리한다(객체로 반환). 또한, useState, useEffect등의 훅을 이용할 필요도 없다. 코드로 알아보자.
<br /></p>
<ul>
<li>Fetch API를 사용<pre><code>import React, { useEffect, useState } from 'react';
</code></pre></li>
</ul>
<p>function FetchExample() {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);</p>
<p>  useEffect(() =&gt; {
    setLoading(true);
    fetch('<a href="https://api.example.com/data'">https://api.example.com/data'</a>)
      .then((response) =&gt; {
        if (!response.ok) throw new Error('Network response was not ok');
        return response.json();
      })
      .then((data) =&gt; setData(data))
      .catch((error) =&gt; setError(error))
      .finally(() =&gt; setLoading(false));
  }, []);</p>
<p>  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;
  return <div>Data: {JSON.stringify(data)}</div>;
}</p>
<pre><code>위 useQuery의 예시를 Fetch API로 구현했을 때의 코드이다. Fetch API를 사용하면 받아올 데이터, loading, error의 상태를 모두 선언 후 처리해주어야 한다. 반면, useQuery는 </code></pre><p>  const { data, isLoading, error } = useQuery('data', fetchData);</p>
<pre><code>이 코드 한줄로 위 과정을 대체한다.

추가로, 컴포넌트가 마운트 될 때마다 실행되어야 하기 때문에, useEffect를 사용했지만, useQuery는 해당 기능을 자동으로 제공하기 때문에 useEffect를 사용할 필요도 없다. 결과적으로, useState, useEffect 등을 사용할 필요가 없으니, 코드가 간결해지고 가독성이 높아진다.
&lt;br /&gt;
&lt;hr /&gt;
&lt;br /&gt;

### 4. 프로젝트 적용에 대한 고민

현재 주차장 예약 및 주차 요금 정산 어플 프로젝트 중에 있습니다. 해당 서비스에서도 서버로의 많은 API요청이 있을 예정인데, 서버에 무리를 주지 않는 선에서 사용자 경험을 최대로 올리는 것이 제가 React-Query를 택한 이유이자 목표입니다.

말씀 드린대로, 많은 API 요청이 있는데, 그중 트래픽이 가장 몰릴 것으로 예상되는 기능에 대해 상태관리를 어떻게 해야할지 고민해보았습니다.

1) 주차 요금 조회 기능

![](https://velog.velcdn.com/images/shipleaf/post/52067a72-ed25-474f-adff-c3b193a6f632/image.png)

첫 번째 기능은 주차 요금 정산 기능입니다. 해당 기능이 저희 서비스의 핵심 기능이기도 하고, 메인 화면에 있는 만큼 사용자에게 가장 많이 노출될 것으로 보여 먼저 고민해보게 되었습니다.

주차 요금이 컴포넌트 첫 마운트시 한번 업데이트 되고 만다면, 실제 결제금액과 차이가 나는 경우가 생기기 때문에, 주기적으로 값을 업데이트 해주어야 할 필요가 있습니다.

아직 주차장 요금 정산 방식을 제대로 파악하지 못했지만, 적절한 사용자 경험을 위해서는 최소 1분의 시간 안에는 re-fetch가 이루어져야 할 것 같습니다. 따라서,
</code></pre><p>const { data, isLoading } = useQuery('parkingSlots', fetchParkingSlots, {
  refetchInterval: 60000, // 1분마다 새로고침
});</p>
<pre><code>useQuery, options의 객체인 refetchInterval(re-fetch 간격 설정)을 60000ms(1분)로 설정하고, 창이 내려가거나 꺼지면 요청을 멈춥니다.
&lt;br /&gt;

2) 주차장 예약 기능

![](https://velog.velcdn.com/images/shipleaf/post/273aed9a-9a8f-4388-8141-f6828c3062e0/image.png)

다음으로, 주차장 예약을 위해 남은 주차 공간을 조회하는 API 요청입니다. 해당 정보는 우리 서비스의 서버에서는 조회할 수 없고, 회사의 중앙 데이터베이스에서 조회할 수 있는 정보이기 때문에 메인 화면에 있는 기능이지만, API 요청이 과도하게 몰리면 안됩니다.

따라서, 해당 기능은 조금 불편을 감수하더라도 새로고침 버튼을 두어 자동으로 re-fetch 되지 않으면서 남은 주차공간에 대한 업데이트가 되어야 할 것 같습니다.

&lt;br /&gt;
&lt;hr /&gt;
&lt;br /&gt;

### 5. 마무리

이 글을 작성하기 위해 React-Query를 공부했을 때, 짧은 시간임에도 기존 방식과의 차별점이나 편의성을 알 수 있었던 것 같습니다. 기회가 된다면 프로젝트에 React-Query를 적용한 결과물도 작성해보려고 합니다.

- 참고:
&gt; - [React-query를 사용해 상태관리를 해보자](https://musma.github.io/2023/09/14/react-query.html)
</code></pre>
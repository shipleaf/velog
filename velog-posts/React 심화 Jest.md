<h4 id="예시-1">예시 1.</h4>
<pre><code>// math.js
export function add(a, b) {
  return a + b;
}</code></pre><pre><code>// math.test.js
import { add } from './math';

test('adds 1 + 2 to equal 3', () =&gt; {
  expect(add(1, 2)).toBe(3);
});</code></pre><h4 id="예시-2">예시 2.</h4>
<pre><code>// Hello.jsx
import React from 'react';

const Hello = ({ name }) =&gt; {
  return &lt;h1&gt;Hello, {name}!&lt;/h1&gt;;
};

export default Hello;</code></pre><pre><code>// Hello.test.jsx
import { render, screen } from '@testing-library/react';
import Hello from './Hello';

test('renders the correct greeting', () =&gt; {
  render(&lt;Hello name=&quot;World&quot; /&gt;);
  const greetingElement = screen.getByText(/Hello, World!/i);
  expect(greetingElement).toBeInTheDocument();
});</code></pre><h4 id="예시-3">예시 3.</h4>
<pre><code>// fetchData.js
export async function fetchData() {
  const response = await fetch('/api/data');
  return response.json();
}</code></pre><pre><code>// fetchData.test.js
import { fetchData } from './fetchData';

jest.mock('./fetchData'); // fetchData 함수를 Mocking

test('fetchData returns mocked data', async () =&gt; {
  fetchData.mockResolvedValue({ data: 'mocked data' });
  const result = await fetchData();
  expect(result).toEqual({ data: 'mocked data' });
});</code></pre>
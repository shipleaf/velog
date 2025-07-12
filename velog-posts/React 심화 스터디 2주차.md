<h3 id="1강-react-개요">1강. React 개요</h3>
<ul>
<li><p>Virtual Dom 개념:
React 컴포넌트가 처음 렌더링 될 때, 실제 Dom의 복사본인 Virtual Dom을 생성, 컴포넌트의 상태가 업데이트 될 때 새로운 Virtual Dom을 생성하여 기존 Virtual Dom과 비교 후 차이점을 찾아 실제 Dom에 반영할 때 차이점만 찾아 효율적으로 수정한다.</p>
</li>
<li><p>JSX의 사용</p>
</li>
</ul>
<h3 id="2강-react-프로젝트-만들기">2강. React 프로젝트 만들기</h3>
<pre><code>React with Babel [es6, jsx]

- module bundler
  - webpack 2
  - webpack-dev-server

- loader
  - babel-loader    // jsx를 javascript로 변환해주는 자바스크립트용 컴파일러
    - babel-core
    - babel-preset-env
    - babel-plugin-transform-react-jsx

- react
  - react
  - react-dom</code></pre><pre><code>  React with TypeScript [ts, tsx]

- module bundler
  - webpack 2
  - webpack-dev-server

- loader
  - ts-loader    // typescript를 javascript로 변환해주는 모듈
    - typescript
  - tslint-loader    // jsx의 eslint, 오류를 잡아주는 도구
    - tslint
    - tslint-react
  - source-map-loader

- react
  - react, @types/react
  - react-dom, @types/react-dom</code></pre><p>  <img alt="" src="https://velog.velcdn.com/images/shipleaf/post/8d430e12-5420-40a5-a8d4-be45cbb9a5ba/image.png" /></p>
<p>next.js는 내부적으로 typescript를 지원하고, webpack을 포함하기 때문에 ts-loader와 같은 도구가 필요하지 않지만, react는 webpack을 포함하지 않기 때문에 webpack으로 번들링을 해줄 ts-loader같은 도구가 필요하다.</p>
<p>+ react 폴더 구조에서 src에 있는 코드를 ts-loader를 통해 컴파일 된 파일이 dist로 이동, 렌더링 된다.</p>
<h3 id="3강-create-react-app">3강. create-react-app</h3>
<pre><code>npm i install create-react-app -g</code></pre><p>해당 명령어는 이제 지원하지 않는다. 대신 아래 명령어를 이용한다.</p>
<pre><code>npx create-react-app my-app</code></pre><p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/2a4a16b8-0c97-4492-b7e9-141463b3fe54/image.png" /></p>
<p>tslint에 대한 파일이 없는데, tslint는 2019년도 이후에 eslint로 통합되었다.</p>
<pre><code>npm install eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin --save-dev
</code></pre><blockquote>
<p>eslintrc.json
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/f66ed279-c64c-47e9-8776-61814683f7ef/image.png" /></p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/2b4c674b-d4ae-454f-ab69-9da1972c8787/image.png" /></p>
<h3 id="섹션2-component">섹션2. Component</h3>
<p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/1bb5337b-15fe-4248-85e4-853588bfb8c2/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/41551168-88fd-4c60-bb7e-7f2e6386e9c4/image.png" /></p>
<ul>
<li>Statelesscomponent도 React Hooks의 개발로 의미가 없어져 사용하지 않게됨</li>
</ul>
<pre><code>const FilterButton = ({ onClick, isActive, prop }) =&gt; {
    return (
        &lt;Button onClick={onClick} isActive={isActive}&gt;
            &lt;CheckIcon&gt;&amp;#128504;&lt;/CheckIcon&gt;
            {prop}
        &lt;/Button&gt;
    );
};</code></pre><p>함수를 props로 전달하는 구조 예시</p>
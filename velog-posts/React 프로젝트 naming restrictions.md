<p>클론 코딩을 목적으로 React 프로젝트를 만드는 과정에서 naming restriction이 발생했다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/92edba75-a1de-4371-964a-57143036c89f/image.png" /></p>
<p>찾아보니 CRA(Create-React-App)는 아래의 네이밍 규칙을 따라야한다.</p>
<blockquote>
<ol>
<li>공백: 프로젝트 이름에는 공백이 포함되어서는 안된다. 공백 대신에 대시(-)나 언더바(_) 등을 사용해야 한다.</li>
<li>특수 문자: 일반적으로 특수 문자는 허용되지 않는다. 알파벳 문자, 숫자, 대시, 언더스코어만을 사용해야 한다.</li>
<li>숫자로 시작: 프로젝트 이름은 숫자로 시작할 수 없다.</li>
<li>NPM 규칙: 프로젝트 이름은 NPM 규칙을 따라야 한다. NPM 규칙에 따르면 소문자만 사용해야 하고, 단일 단어가 아닌 경우에는 대시나 언더스코어를 사용하여 단어를 구분한다.</li>
</ol>
</blockquote>
<p>해결 완료!</p>
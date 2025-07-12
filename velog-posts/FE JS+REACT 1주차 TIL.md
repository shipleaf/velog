<h2 id="1-개발-환경-설정하기">1. 개발 환경 설정하기</h2>
<p>Node.js는 JavaScript로 네트워크 어플리케이션을 개발할 수 있도록 하는 개발 환경을 말합니다.
npm(node package manager)은 node.js의 패키지 다운로드 같은 기능을 지원하는 개발 도우입니다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/2580c197-9c29-4493-bb28-fc0d6b8cce19/image.png" />
node.js와 npm을 홈페이지에서 LTS(장기 지원 버전)를 선택해서 다운로드 했습니다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/2cfec347-555c-493a-b915-c1154ecf9ffd/image.png" />
저는 VSC가 미리 깔려있어서 VSC 내장터미널로 node.js와 npm 버전 체크를 했습니다.</p>
<h2 id="2-html--css-복습">2. HTML &amp; CSS 복습</h2>
<h4 id="htmlhypertext-markup-language은-웹사이트의-뼈대를-구성하기-위해-사용하는-마크업-언어로-태그를-사용해서-구조와-내용을-만듭니다">HTML(HyperText Markup Language)은 웹사이트의 뼈대를 구성하기 위해 사용하는 마크업 언어로, 태그를 사용해서 구조와 내용을 만듭니다.</h4>
<pre><code>&lt;html&gt;
    &lt;head&gt;&lt;/head&gt;
    &lt;body&gt;&lt;/body&gt;
&lt;/html&gt;</code></pre><p>html 문서의 뼈대를 구성하는 태그들입니다. head태그는 웹사이트의 제목, 설명과 같은 속성을 표현합니다. body태그에는 사용자들이 웹사이트에서 보는 컨테츠 내용들이 들어갑니다.</p>
<p>웹사이트를 구성하는 html 문서의 보관이 까다롭기 때문에 React와 같은 프로그램을 이용해서 SPA 방식으로 웹사이트를 구성합니다. SPA 방식은 body태그가 비어있는 상태에서 콘텐츠를 불러와서 렌더링하는 방식입니다.</p>
<h4 id="csscascading-style-sheets는-웹사이트의-레이아웃과-글꼴-색상-등의-디자인을-입히는-언어입니다">CSS(cascading style sheets)는 웹사이트의 레이아웃과 글꼴, 색상 등의 디자인을 입히는 언어입니다.</h4>
<p>CSS를 사용해서 웹사이트를 꾸밀 수 있습니다. 하지만, 속성이 많기 때문에 외워서 작성하는데에는 한계가 있습니다.</p>
<h2 id="3-js-소개-및-자료형">3. JS 소개 및 자료형</h2>
<h3 id="javascript는-웹사이트에서-버튼을-누르거나-정보를-입력하는-등의-동적인-행동을-수행할-수-있도록-지원하는-프로그래밍-언어입니다">Javascript는 웹사이트에서 버튼을 누르거나 정보를 입력하는 등의 동적인 행동을 수행할 수 있도록 지원하는 프로그래밍 언어입니다.</h3>
<p>Javascipt는 스크립트 언어로 런타임에 프로그램의 해석이 실행됩니다. 버전이 많고 꾸준히 업데이트 하고 있지만, 주로 ES6(ECMAScript 2015)를 사용합니다.</p>
<h3 id="javascript의-자료형">JavaScript의 자료형</h3>
<p>Javascript의 변수는 다른 프로그래밍 언어와 다르게 변수를 선언할 때가 아닌, 변수에 데이터가 대입될 때 자료형이 결정된다(동적 타이핑). 따라서, 변수의 데이터 타입을 지정해주지 않아도 된다.</p>
<p>1) 숫자
2) 문자열
3) Boolean
4) NULL
5) undefined
6) Array
7) Object</p>
<p>위의 자료형 중 NULL과 undefined의 차이점이 조금 헷갈렸는데, undefined은 변수를 선언하고 값을 할당하지 않은 상태, null은 변수를 선언하고 빈 값을 할당한 상태이다. JS에서 object는 key, value로 이루어진 데이터 타입을 말합니다. Python의 dictionary 타입과 유사합니다.</p>
<h2 id="4-js의-연산자">4. JS의 연산자</h2>
<h4 id="1-대입-연산자">1. 대입 연산자</h4>
<p>예시)
    a = 10;
대입 연산자는 항상 오른쪽에서 왼쪽으로 흐름이 흘러갑니다. 위의 식을 예시로 들면 변수 a가 10에 대입되는 것이 아닌, 정수 10이 변수 a에 대입된다는 뜻입니다.</p>
<h4 id="2-사칙-연산자">2. 사칙 연산자</h4>
<p>+(덧셈), -(뺄셈), <em>(곱셈), /(나눗셈)에 나머지를 구하는 연산자 %, 제곱을 구하는 연산자 *</em> 등이 있다.</p>
<h4 id="3-증감-연산자">3. 증감 연산자</h4>
<ul>
<li>postfix 방식: a++</li>
<li>prefix 방식: ++a
두 방식의 차이는 처리 순서로 postfix는 a값을 반환 후 더하고, prefix는 값을 더한 후에 a값을 반환합니다.<h4 id="4-비교-연산자">4. 비교 연산자</h4>
&lt;, &lt;=, &gt;, &gt;= 와 같은 연산자들로 왼쪽 항과 오른쪽 항의 값을 비교합니다.<h4 id="5-동등-연산자">5. 동등 연산자</h4>
예시)<pre><code>a == b
a != b</code></pre>동등 연산자는 왼쪽 항과 오른쪽 항의 값이 같다 혹은 다르다의 결과를 boolean 형태로 return 합니다.<h4 id="6-일치-연산자">6. 일치 연산자</h4>
일치 연산자는 동등 연산자에 더해 자료형까지 비교합니다.<pre><code>a === b
a !== b</code></pre><h4 id="7-이진-논리-연산자">7. 이진 논리 연산자</h4>
</li>
<li>a &amp;&amp; b: a와 b 값 모두 True일 경우 True를 반환합니다.</li>
<li>a || b: a와 b 값 둘 중 하나가 True일 경우 True를 반환합니다.<h4 id="8-조건부-연산자삼항-연산자">8. 조건부 연산자(삼항 연산자)</h4>
예시)
  console.log(a? 1 : 2);</li>
<li><blockquote>
<p>조건식이 True일 경우 1을, False일 경우 2를 리턴합니다.</p>
</blockquote>
</li>
</ul>
<h2 id="5-font-awesome-실습">5. font awesome 실습</h2>
<p>Icon은 웹사이트를 좀 더 다채롭게 만듭니다. font awesome은 icon을 무료로 지원하는 웹사이트 입니다.</p>
<h4 id="font-awesome-사용방법">font awesome 사용방법</h4>
<ol>
<li><p>font awesome 홈페이지에서 kit를 복사 후 html 문서의 head 태그에 붙여넣기 합니다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/457378cc-bc14-4da3-ae9c-270f41f6152f/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/41d460dc-1e91-4f53-8e57-9283a1962849/image.png" /></p>
</li>
<li><p>font awesome icon 탭에서 Free icon 옵션으로 들어갑니다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/60800da2-b816-4867-8274-5e8b1b3bee58/image.png" /></p>
</li>
<li><p>원하는 아이콘의 i 태그를 복사한 후 html 문서에 붙여넣기 해줍니다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/beda4438-8152-452f-81e4-03dcf7d8867c/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/0ece77cf-cf00-4e85-9619-91d866cb1272/image.png" /></p>
</li>
</ol>
<p>아래 사진과 같이 웹페이지에 icon이 표시됩니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/f8428691-7aa6-4930-bda6-30676c16073d/image.png" /></p>
<h2 id="6-1주차-알고리즘-문제숙제">6. 1주차 알고리즘 문제(숙제)</h2>
<h4 id="1-정수-num1-num2가-매개변수로-주어질-때-num1을-num2로-나눈-몫을-return-하도록-solution-함수를-완성해주세요">1) 정수 num1, num2가 매개변수로 주어질 때, num1을 num2로 나눈 몫을 return 하도록 solution 함수를 완성해주세요.</h4>
<p>풀이: 주어진 숫자와 같거나 작은 정수를 반환하는 Math.floor 함수에 매개변수 num1, num2를 대입하여 풀이합니다.</p>
<pre><code>function solution (num1, num2) {
    var answer = Math.floor(num1/num2);
    return answer;
}</code></pre><p>풀이 확인:
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/4c4db465-8b3b-4945-960c-fc67caee9b8e/image.png" />
consloe.log 함수를 이용해서 num1에 100, num2에 20을 대입하면
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/124aa78f-aa34-4604-8275-552fd6f37423/image.png" />
위 사진처럼 5의 결과가 나옵니다.</p>
<h4 id="2-정수-num1과-num2가-매개변수로-주어집니다-두-수가-같으면-1-다르면--1을-retrun하도록-solution-함수를-완성해주세요">2) 정수 num1과 num2가 매개변수로 주어집니다. 두 수가 같으면 1 다르면 -1을 retrun하도록 solution 함수를 완성해주세요.</h4>
<p>풀이: If 조건문을 사용해서 num1과 num2가 같을 때 1을 return, 다를 때 -1을 return 하도록 풀이합니다.</p>
<pre><code>function solution (num1, num2) {
    if (num1 === num2) {
        return 1
    }
    return -1
}</code></pre><p>풀이 확인: 
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/39d855ed-54b3-4d76-8adf-951f950593e1/image.png" />
console.log 함수에 각각 (10,10), (10,1)을 대입하면, 아래의 결과가 나옵니다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/714f0bac-ee50-42b7-839b-27e3f1b7e9f4/image.png" /></p>
<h4 id="3-머쓱이는-선생님이-몇-년도에-태어났는지-궁금해졌습니다-2022년-기준-선생님의-나이-age가-주어질-때-선생님의-출생-연도를-return-하는-solution-함수를-완성해주세요">3) 머쓱이는 선생님이 몇 년도에 태어났는지 궁금해졌습니다. 2022년 기준 선생님의 나이 age가 주어질 때, 선생님의 출생 연도를 return 하는 solution 함수를 완성해주세요</h4>
<p>풀이: 2022년을 기준으로 출생년도는 2022 - 나이 + 1 이므로 return 값을 2022 - age + 1로 풀이합니다.</p>
<pre><code>function solution (age) {
    var birth = 2022 - age + 1;
    return birth;
}</code></pre><p>풀이 확인:
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/1fc6e3a1-75bc-44e9-9f77-d0c8388d958e/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/348afce9-a1bc-434a-bf52-c8e985892028/image.png" /></p>
<p>console.log 함수에 나이 54를 대입하면, 위의 결과가 나옵니다.</p>
<h4 id="4-각에서-0도-초과-90도-미만은-예각-90도는-직각-90도-초과-180도-미만은-둔각-180도는-평각으로-분류합니다-각-angle이-매개변수로-주어질-때-예각일-때-1-직각일-때-2-둔각일-때-3-평각일-때-4를-return하도록-solution-함수를-완성해주세요">4) 각에서 0도 초과 90도 미만은 예각, 90도는 직각, 90도 초과 180도 미만은 둔각 180도는 평각으로 분류합니다. 각 angle이 매개변수로 주어질 때 예각일 때 1, 직각일 때 2, 둔각일 때 3, 평각일 때 4를 return하도록 solution 함수를 완성해주세요.</h4>
<p>풀이: 3번과 마찬가지로 if문을 사용하여 예각, 직각, 둔각, 평각일 때 4가지 케이스로 나눠서 return 값을 설정하는 방법으로 풀이한다.</p>
<pre><code>function solution (angle) {
    if (angle &gt; 0 &amp;&amp; angle &lt; 90){
        return 1
    } else if (angle == 90) {
        return 2
    } else if (angle &gt; 90 &amp;&amp; angle &lt; 180) {
        return 3
    } else if (angle == 180) {
        return 4
    }
}</code></pre><p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/451f9cd2-5827-475b-a647-66f851711e81/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/b4bb490f-d1ee-4a73-ace2-52b84c7358c1/image.png" />
console.log 함수에 각각 60, 90, 100, 180도를 대입하면 위의 결과가 나옵니다.</p>
<h4 id="5-머쓱이네-양꼬치-가게는-10인분을-먹으면-음료수-하나를-서비스로-줍니다-양꼬치는-1인분에-12000원-음료수는-2000원입니다-정수-n과-k가-매개변수로-주어졌을-때-양꼬치-n인분과-음료수-k개를-먹었다면-총얼마를-지불해야-하는지-return-하도록-solution-함수를-완성해보세요">5) 머쓱이네 양꼬치 가게는 10인분을 먹으면 음료수 하나를 서비스로 줍니다. 양꼬치는 1인분에 12,000원, 음료수는 2,000원입니다. 정수 n과 k가 매개변수로 주어졌을 때, 양꼬치 n인분과 음료수 k개를 먹었다면 총얼마를 지불해야 하는지 return 하도록 solution 함수를 완성해보세요.</h4>
<p>풀이: 양꼬치 개수인 n이 10보다 크면 n을 10으로 나눠 몫을 구하고 음료수 서비스 개수를 구합니다. n이 10보다 작으면 음료수 서비스 없이 금액을 계산합니다.</p>
<pre><code>function solution (n, k) {
    if (n &gt;= 10) {
        var service = Math.floor(n/10);
        var total = (n * 12000) + (k * 2000) - (service * 2000);
        return total;
    } else {
        var total = (n * 12000) + (k * 2000);
        return total;
    };
}</code></pre><p>풀이 확인: 
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/d922b391-35c5-47a7-86a0-00ebebaa2903/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/6c1ecf49-da88-4af3-8f47-594f81d5102c/image.png" />
console.log에 함수에 위 사진의 값을 입력하면 아래 사진의 결과가 나옵니다.</p>
<h4 id="6-정수-n이-주어질-때-n이하의-짝수를-모두-더한-값을-return-하도록-solution-함수를-작성해주세요">6) 정수 n이 주어질 때, n이하의 짝수를 모두 더한 값을 return 하도록 solution 함수를 작성해주세요.</h4>
<p>풀이: 정수 n 이하의 수 중에 2로 나눴을 때 나머지가 0인 값들을 반복문을 통해 더해서 구합니다.</p>
<pre><code>function solution (n) {
    var total = 0;
    for (var i = 1; i &lt;=n; i++) {
        if (i % 2 == 0) {
            total += i;
        }
    }
    return total;
}</code></pre><p>풀이 확인:
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/38169b89-9a7b-4217-ad0f-3d8e11db038a/image.png" />
console.log에 13을 대입하면, 아래 사진의 결과가 나옵니다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/a36b7423-f4e3-47b0-af1b-8214f0e3603e/image.png" /></p>
<h2 id="7-javascript의-함수">7. Javascript의 함수</h2>
<p>함수는 parameter를 입력받아 정해진 출력을 하는 도구입니다.</p>
<h4 id="javascript-함수-선언-방법">Javascript 함수 선언 방법</h4>
<p>1) function statement</p>
<pre><code>예시)
function sum(a+b) {
    return a+b;
}</code></pre><p>function statement는 위와 같이 function 함수명(인자) {출력 내용}으로 구성됩니다.</p>
<p>2) arrow function expression</p>
<pre><code>예시)
const multifly = (a, b) =&gt; {
    return a * b;
}</code></pre><p>화살표 함수는 const 함수명 = (인자) =&gt; {출력 내용} 으로 구성됩니다.</p>
<p>두 방식은 hoistng 지원 여부로 구분된다.
function statement 방식은 hoisting을 지원하기 때문에</p>
<pre><code>console.log(sum(3, 4))

function sum(a, b){
    return a+b;
}</code></pre><p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/b94de1af-a967-46e6-bc02-eca230f60c19/image.png" /></p>
<p>함수 위에 출력문을 적어도 위 사진처럼 결과가 나옵니다.</p>
<p>반면, 화살표 함수는 hoisting 방식을 지원하지 않기 때문에 출력문을 반드시 함수 아래에 적어줘야 합니다.</p>
<h2 id="8-리엑트는-무엇인가">8. 리엑트는 무엇인가</h2>
<p>React는 user interfaces를 만들기 위한 javascript 라이브러리입니다.
라이브러리는 프로그램 기능 중 자주 사용되는 기능을 모아놓은 것을 말합니다.
React는 대표적인 UI 라이브러리이며, meta의 오픈 소스 프로젝트입니다.</p>
<blockquote>
<h4 id="프레임워크와-라이브러리의-차이점은">프레임워크와 라이브러리의 차이점은?</h4>
<p>프레임워크는 프로그램 흐름의 제어권한을 프레임 워크가 가집니다. 반면, 라이브러리는 흐름에 대한 제어를 하지 않고 개발자가 필요한 부분만 가져다 사용할 수 있습니다.</p>
</blockquote>
<h2 id="9-리엑트의-장점과-단점">9. 리엑트의 장점과 단점</h2>
<h4 id="dom이란">DOM이란?</h4>
<p>웹페이지를 정의하는 하나의 객체, 하나의 웹페이지에 대한 정보를 모두 담고있는 큰 그릇입니다.</p>
<h3 id="리엑트의-장점">리엑트의 장점</h3>
<h4 id="1-빠른-업데이트와-렌더링-속도">1. 빠른 업데이트와 렌더링 속도</h4>
<p>일반적인 웹사이트는 웹페이지를 수시로 업데이트(DOM 변경)하여 성능에 영향을 미치고 비용을 증가시킵니다(수정할 부분을 DOM 데이터에서 찾아야 하기 때문). 반면, React는 DOM 수정을 하지 않고 업데이트 해야할 부분만 검색, 검색된 부분만 업데이트 후 다시 렌더링 하는 방식으로 빠른 속도를 가집니다. </p>
<h4 id="2-component-based">2. Component-Based</h4>
<p>React의 모든 페이지는 component로 구성되며, 하나의 component는 여러 개의 component로 구성됩니다. 이러한 React의 특징은 프로그램의 재사용성을 늘려줍니다.
따라서 개발 기간이 단축되고 프로그램의 유지, 보수가 용이합니다.</p>
<p>  프로그램의 재사용성은 모듈 간의 의존성 등 여러 가지를 고려해야 합니다. 즉, 재사용이 가능하다는 것은 모듈이 다른 곳에도 쉡게 재사용 될 수 있도록 개발하는 것을 의미합니다.</p>
<h4 id="3-든든한-지원군">3. 든든한 지원군</h4>
<p>React는 Meta의 오픈소스 프로젝트입니다. Meta는 React에 많은 투자를 하고 지속적으로 업데이트하고 있기 때문에 믿고 사용할 수 있습니다.</p>
<h4 id="4-활발한-지식공유--커뮤니티">4. 활발한 지식공유 &amp; 커뮤니티</h4>
<p>프로그램을 사용하다 모르는 것이 있으면 공유할 수 있는 커뮤니티가 필요합니다. React는 github, stackoverflow등 개발자 커뮤니티에서 인기가 있는 라이브러리이기 때문에 모르는 부분에 대한 지식을 얻기 비교적 쉽습니다.</p>
<h4 id="5-react-native">5. React Native</h4>
<p>React Native는 js코드로 모바일 앱 개발을 할 수 있는 도구로 ios와 안드로이드 모두 사용 가능한 앱을 만들 수 있습니다.</p>
<h3 id="리엑트의-단점">리엑트의 단점</h3>
<h4 id="1-방대한-학습량">1. 방대한 학습량</h4>
<p>React는 기존 방식들과 다른 라이브러리이고 업데이트가 활발하기 때문에 학습량이 많습니다. </p>
<h4 id="2-높은-상태관리-복잡도">2. 높은 상태관리 복잡도</h4>
<h4 id="state-react-component의-상태">&gt; state: react component의 상태</h4>
<p>React는 component 단위로 이루어진 라이브러리이기 때문에 component 개수가 늘어날수록 상태관리 복잡도가 높아집니다. 높은 상태관리 복잡도 때문에 개발자들은 외부 상태관리 라이브러리를 사용하기도 합니다.</p>
<h2 id="10-직접-리엑트-연동하기">10. 직접 리엑트 연동하기</h2>
<p>간단한 HTML 웹 사이트를 만들어 리엑트를 연동해봤습니다.</p>
<pre><code>&lt;html&gt;
    &lt;head&gt;
        &lt;title&gt;선엽의 블로그&lt;/title&gt;
        &lt;link rel=&quot;stylesheet&quot; href=&quot;./style.css&quot;&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;h1&gt;선엽의 블로그에 오신 것을 환영합니다!&lt;/h1&gt;

        &lt;div id=&quot;root&quot;&gt;&lt;/div&gt;


    &lt;/body&gt;
&lt;/html&gt;</code></pre><p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/d742b16a-bcce-496f-a87b-53a5af6732be/image.png" />
html 문서를 이용해 위와 같은 웹사이트를 만들고</p>
<pre><code>h1 {
    color: green;
    font-style: italic;
}</code></pre><p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/cefee76f-948f-4153-ac6a-3af4106fe373/image.png" />
css를 통해 스타일을 변경해줬습니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/5f93c74f-d127-4bec-b8be-7d628d6a6166/image.png" />
React 연동을 위해 body 태그 내부에 script 태그를 이용해 react url을 연결했습니다.</p>
<pre><code>function Mybutton(props) {
    const [isClicked, setIsClicked] = React.useState(false);

    return React.createElement (
        'button',
        { onClick: () =&gt; setIsClicked(true) },
        isClicked ? 'Clicked!' : 'Click here!'
    )
}

const domContainer = document.querySelector('#root');
ReactDOM.render(React.createElement(Mybutton), domContainer);</code></pre><p>react.createElement 함수를 이용해 버튼을 생성하는 js 코드를 작성했습니다.</p>
<p>클릭 전:
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/522a12b0-b300-44a1-bb2f-2a6d91e1b958/image.png" /></p>
<p>클릭 후:
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/75eba3a6-22f1-4084-b3c3-26e03b88de33/image.png" /></p>
<p>완성:
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/5f615517-20ba-43a4-b3cb-771179a3ddf8/image.png" /></p>
<h2 id="11-create-react-app">11. create-react-app</h2>
<p>앞의 예시는 기존 웹사이트에 React를 연동하는 것입니다. React를 새로운 웹사이트에 적용하는 방법을 알아보겠습니다.</p>
<ol>
<li>npx create-react-app &lt;프로젝트먕&gt; 을 VSC 터미널에 입력해 줍니다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/9061fde6-814a-4ca6-920a-16b9fc155cd7/image.png" /></li>
<li>로딩이 완료 되면 cd(경로 변경) 명령어와 npm start(실행) 명령어를 입력할 수 있습니다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/f4bd9ede-4c5f-44ff-9f84-7883465acf91/image.png" />
node.js 삭제 후 재설치를 해도 -4058 에러가 발생했습니다.
알고보니 package.json이라는 파일이 있는 폴더를 직접 지정해줘야 실행을 할 수 있었습니다.
cd 명령어를 이용하여 폴더를 바꾸고 npm start를 입력하니, 
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/d84a8004-d538-42f1-958b-d925fc8e0bed/image.png" />
강의 내용과 같이 react 실행이 완료 되었습니다.</li>
</ol>
<h2 id="12-화살표-함수">12. 화살표 함수</h2>
<p>함수식은 함수 선언식과 함수 호출식으로 나뉘는데, 일반 함수의 경우는 hoisting(화면 상단에 함수가 위치하도록 지원)을 지원하기 때문에 호출식을 선언식보다 위에 적을 수 있습니다. 하지만, 함수명을 필요로 하기 때문에 익명 함수를 만들 수 없습니다.</p>
<p>익명 함수를 만들기 위해서는 함수 표현식을 사용하면 됩니다.
예시)</p>
<pre><code>const main = function() {
    console.log(&quot;Hello&quot;)
}</code></pre><p>함수 표현식은 함수 선언식과 다르게 hoisting을 지원하지 않습니다. 때문에, 표현식 상단에 함수를 호출할 수 없습니다.</p>
<p>화살표 함수는 기존의 함수 표현식을 더 간결하게 작성할 수 있도록 해줍니다.
예시)</p>
<pre><code>const main = () =&gt; {
    console.log(&quot;hello&quot;)
}</code></pre><p>함수의 코드가 한줄이면 return과 중괄호를 생략할 수 있고 자동으로 값을 return해줍니다.
예시)</p>
<pre><code>const add = (a, b) =&gt; a + b
const main = () =&gt; console.log(&quot;hello&quot;)</code></pre><p>매개변수가 하나라면 소괄호도 생략 가능합니다. 하지만, 매개변수가 하나도 없거나 두 개 이상인 경우는 생략이 불가능하다.</p>
<p>객체를 리턴할 때는 소괄호로 한번 감싸준다.
예시)</p>
<pre><code>const getObject = () =&gt; ({name:&quot;김선엽&quot;})</code></pre><p>화살표 함수와 일반함수의 차이점은 코드의 간결함 이외에도 arguments(인자) 개념의 차이도 있습니다. 일반 함수는 함수 선언시 변수가 없더라도 암묵적으로 argument에 인자를 포함시킵니다. 반면 화살표 함수는 인자가 자동으로 포함되지 않습니다. 화살표 함수에 인자를 포함시키려면 함수 선언시 (...변수명) 을 화살표 함수 arguments에 대입해야 합니다.</p>
<h2 id="13-jsx의-정의와-역할">13. JSX의 정의와 역할</h2>
<p>JSX는 Javascript 문법의 확장된 영역으로, Javascript와 XML/HTML을 섞어 사용합니다.
예시)</p>
<pre><code>const element = &lt;h1&gt;hello, world!&lt;/h1&gt;;</code></pre><blockquote>
<h4 id="jsx를-사용하는-이유는">JSX를 사용하는 이유는?</h4>
<p>JSX는 내부적으로 createElement 함수를 이용해서 HTML/XML 코드를 JS로 변환하는 과정을 거칩니다. 때문에 JSX를 사용하는 것은 필수가 아니지만, JSX를 사용하면 많은 장점들이 있습니다.</p>
</blockquote>
<h2 id="14-jsx의-장점-및-사용법">14. JSX의 장점 및 사용법</h2>
<h3 id="js의-장점">JS의 장점</h3>
<ol>
<li><p>간결한 코드
예시)
```</p>
</li>
<li><p>JSX</p>
<div>Hello, {name}</div></li>
<li><p>JSX 사용 안함
React.createElement('div', null, 'Hello, ${name}');</p>
<pre><code>코드 예시로도 보이듯이 JSX 코드는 JSX를 사용하지 않은 코드에 비해 간결합니다.</code></pre></li>
<li><p>가독성 향상
마찬가지로 코드가 가독성이 좋습니다. 때문에 유지 보수 및 버그 발견 등에 용이합니다.</p>
</li>
<li><p>Injection Attacks 방어에 용이
입력창에 문자나 숫자같은 일반적인 입력 값이 아닌, 소스코드를 입력하여 프로그램을 해킹하는 방법인 injection attack에 대한 방어에 유리합니다.</p>
</li>
</ol>
<h3 id="jsx-사용법">JSX 사용법</h3>
<h4 id="jsx-코드는-js-코드--xmlhtml로-이루어져-있습니다-보통-중괄호를-사용하여-js코드를-표시합니다">JSX 코드는 JS 코드 + XML/HTML로 이루어져 있습니다. 보통 중괄호를 사용하여 JS코드를 표시합니다.</h4>
<p>예시)</p>
<pre><code>    XML/HTML
        {JS 코드}
    XML/HTML</code></pre><p>위의 예시 말고도, HTML 코드 중간이 아닌 속성에 값을 넣으려면</p>
<h4 id="1-큰따옴표-사이에-문자열을-넣기">1. 큰따옴표 사이에 문자열을 넣기</h4>
<p>예시)</p>
<pre><code>const element = &lt;div tabIndex=&quot;0&quot;&gt;&lt;/div&gt;</code></pre><h4 id="2-중괄호-사이에-js-코드-넣기">2. 중괄호 사이에 JS 코드 넣기</h4>
<p>예시)</p>
<pre><code>const element = &lt;img src = {user.avatorUrl}&gt;&lt;/img&gt;;</code></pre><p>위 세 가지 방식으로 JSX 코드를 작성합니다.</p>
<h2 id="15-jsx-코드-작성해보기">15. JSX 코드 작성해보기</h2>
<h3 id="jsx-코드-실습">JSX 코드 실습</h3>
<ol>
<li><p>create-react-app을 통해 설치한 폴더에 Book.jsx 파일을 생성하고 코드를 작성합니다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/60100e95-bb87-4dad-acb2-af3a1a4f6ac7/image.png" /></p>
</li>
<li><p>Book.jsx의 상위 component인 Library.jsx를 생성하고 코드를 작성합니다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/6c928f12-0319-4aa1-abdc-86e6d2652511/image.png" /></p>
</li>
<li><p>렌더링을 위해 index.js 파일을 수정합니다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/8ad7a228-ffd9-4096-8a6b-7a27813e1606/image.png" /></p>
</li>
<li><p>결과
결과를 출력할 때 결과창이
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/238264ae-145e-4870-b853-2f2904367f42/image.png" />
위 처럼 나와서 당황했는데
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/bfb45c84-310f-4bff-b00d-8a445f72c803/image.png" />
위 코드 중 JS 코드의 내부에 작은 따옴표(') 대신 백틱(`)이 들어가야 코드가 정상 작동하는 것을 파악했습니다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/7aee7221-6773-4431-a6ff-b112cebdd918/image.png" /></p>
</li>
</ol>
<h2 id="16-나머지-매개변수와-spread-연산자">16. 나머지 매개변수와 spread 연산자</h2>
<p>Javascript는 함수  인자에 개수 제한이 없지만, 출력은 제한됩니다.
함수에 인자를 넣는 2가지 방법으로는 1. arguments 2. 나머지 매개변수가 있습니다.
나머지 매개변수를 통해 단일 변수로 여러 개의 인자를 받고 출력할 수 있습니다.
나머지 매개변수는 (...변수명) 으로 쓰입니다.</p>
<p>전개 구문(spread syntax)를 이용해 배열을 풀어쓰는 것도 가능합니다.
예시)</p>
<pre><code>let arr1 = [1, 2, 3];
console.log(...arr1) =&gt; [1, 2, 3]</code></pre><p>마찬가지로 객체도 가능합니다.</p>
<h2 id="17-2주차-알고리즘-문제">17. 2주차 알고리즘 문제</h2>
<h4 id="1-정수-배열-numbers가-매개변수로-주어집니다-numbers의-원소의-평균값을-return하도록-solution-함수를-완성해주세요">1. 정수 배열 numbers가 매개변수로 주어집니다. numbers의 원소의 평균값을 return하도록 solution 함수를 완성해주세요.</h4>
<p>풀이: 반복문을 통해 배열의 모든 값을 더하고 배열의 length로 나눠 평균을 구합니다.</p>
<pre><code>function solution(numbers) {
    var sum = 0;
    for(var i = 0; i &lt; numbers.length; i++) {
        sum += numbers[i]
    }
    return (sum/numbers.length)
}</code></pre><p>풀이 확인:
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/fa31dc1e-94d3-443f-bd98-817dcd9ca235/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/f0aea4c4-3220-41f1-a707-83129c894a81/image.png" />
console.log에 배열을 넣으면 아래 사진처럼 결과가 잘 나옵니다.</p>
<h4 id="2-머쓱이는-학교에서-키-순으로-줄을-설-때-몇-번째로-서야-하는지-궁금해졌습니다-머쓱이네-반-친구들의-키가-담긴-정수-배열-array와-머쓱이의-키-height가-매개변수로-주어질-때-머쓱이보다-키-큰-사람-수를-return-하도록-solution-함수를-완성해보세요">2. 머쓱이는 학교에서 키 순으로 줄을 설 때 몇 번째로 서야 하는지 궁금해졌습니다. 머쓱이네 반 친구들의 키가 담긴 정수 배열 array와 머쓱이의 키 height가 매개변수로 주어질 때, 머쓱이보다 키 큰 사람 수를 return 하도록 solution 함수를 완성해보세요.</h4>
<p>풀이: 머쓱이보다 키 큰 사람의 수를 나타내는 변수를 하나 선언하고, for문에 배열을 넣어 머쓱이가 모두 비교 후 더 큰 친구들은 변수에 값을 더하는 방식으로 해결합니다.</p>
<pre><code>function solution(array, height) {
    var answer = 0;
    for(var i=0; i&lt;array.length; i++){
        if (array[i]&gt;height){
            answer++;
        }
    }
    return answer;
}</code></pre><p>풀이 확인:
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/0f7e8d42-5028-428e-9136-21a184e5d624/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/56d5cfd9-51bb-4285-9170-6d1d9206a6e4/image.png" />
175보다 큰 키는 190, 200 두 명이기 때문에 2가 return 되고 있습니다.</p>
<h4 id="3-정수가-담긴-배열-array와-정수-n이-매개변수로-주어질-때-array에-n이-몇-개-있는-지를-return-하도록-solution-함수를-완성해보세요">3. 정수가 담긴 배열 array와 정수 n이 매개변수로 주어질 때, array에 n이 몇 개 있는 지를 return 하도록 solution 함수를 완성해보세요.</h4>
<p>풀이: 변수를 하나 선언하고, 반복문에 배열을 넣어 같은 값이 나올때마다 변수 값에 1을 더해가는 방식으로 풀이합니다.</p>
<pre><code>function solution(array, n) {
    var sum = 0;
    for(var i = 0; i &lt; array.length; i++) {
        if (array[i] == n) {
            sum ++;
        }
    }
    return sum;
}
</code></pre><p>풀이 확인:
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/76db0901-7c70-4aa8-b8da-8aaf47cea197/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/ef0426cf-687b-48d2-8d87-5d86df248e40/image.png" />
10이 3개인 배열이 주어지고 n 값을 10을 주었기 때문에 3이 잘 나왔습니다.</p>
<h4 id="4-머쓱이네-피자가게는-피자를-일곱-조각으로-잘라-줍니다-피자를-나눠먹을-사람의-수-n이-주어질-때-모든-사람이-피자를-한-조각-이상-먹기-위해-필요한-피자의-수를-return-하는-solution-함수를-완성해보세요">4. 머쓱이네 피자가게는 피자를 일곱 조각으로 잘라 줍니다. 피자를 나눠먹을 사람의 수 n이 주어질 때, 모든 사람이 피자를 한 조각 이상 먹기 위해 필요한 피자의 수를 return 하는 solution 함수를 완성해보세요.</h4>
<p>풀이: 주어진 사람의 수 n이 7 * 피자의 수 보다 작으면 되기 때문에 반복문을 사용해서 피자의 수를 늘려가면서 사람의 수와 비교하는 방식으로 풀이한다.</p>
<pre><code>function solution(n) {
    var answer = 0;
    while (n &gt; answer * 7) {
        answer++;
    }
    return answer;
}</code></pre><p>풀이 확인: 
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/157e99c6-5635-496d-a56f-128abf78aef5/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/8e1d04f1-0ce5-4710-b74e-e696aa500ec7/image.png" />
인자로 15를 주었을 때 필요한 피자의 수인 3을 잘 출력하고 있습니다.</p>
<h4 id="5-정수가-담긴-리스트-num_list가-주어질-때-num_list의-원소-중-짝수와-홀수의-개수를-담은-배열을-return-하도록-solution-함수를-완성해보세요">5. 정수가 담긴 리스트 num_list가 주어질 때, num_list의 원소 중 짝수와 홀수의 개수를 담은 배열을 return 하도록 solution 함수를 완성해보세요.</h4>
<p>풀이: 짝수 변수, 홀수 변수를 선언하고 num_list의 원소들을 반복문을 돌려 나머지가 0인 값은 짝수 변수에 + 1 1인 값은 홀수 변수에 + 1 하는 방법으로 풀이한다.</p>
<pre><code>function solution(num_list) {
    var even = 0;
    var odd = 0;
    var List = [];
    for(var i=0; i &lt; num_list.length; i++){
        if(num_list[i] % 2 == 1){
            odd++;
        } else {
            even++;
        }
    }
    List.push(even);
    List.push(odd);
    return List;
}</code></pre><p>풀이 확인:
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/76f44da2-37a8-4877-b084-a0ed4ce4ee37/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/fc646b22-8451-4cb0-80b0-7cc7ad48b04a/image.png" />
인자로 짝수가 3개 홀수가 4개인 배열을 넣어 아래의 결과를 확인했습니다.</p>
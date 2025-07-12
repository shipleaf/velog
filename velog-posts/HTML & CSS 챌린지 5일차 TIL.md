<h3 id="5-display-속성--border-속성">5. Display 속성 &amp; Border 속성</h3>
<p>블록 레벨 요소: 자기가 속한 영역의 너비를 모두 차지하여 블록을 형성한다.
인라인 요소: 자기에게 필요한 만큼의 공간만 차지한다.
display 속성은 요소를 블록과 인라인 요소 중 어느 쪽으로 처리할지 정의한다.</p>
<blockquote>
<h4 id="display-속성-종류">display 속성 종류</h4>
</blockquote>
<ul>
<li>inline: 요소를 인라인 요소로 바꾼다</li>
<li>block: 요소를 블록 요소로 바꾼다</li>
<li>inline-block: 요소를 인라인처럼 배치하되, block의 특성(너비, 높이 조절 가능)을 가지게 바꾼다.</li>
<li>none: 요소를 숨긴다.</li>
</ul>
<blockquote>
<h3 id="border-속성">border 속성</h3>
<p>border 속성을 사용하면 요소가 차지하고 있는 영역에 테두리를 그릴 수 있다. border 속성에는 속성값으로 테두리의 두께, 모양, 크기 등을 함께 지정할 수 있는데, 이러한 속성을 '단축속성'이라 한다.
    예시) span{ border: 2px solid green; }
    단축속성은 따로 지정해줄 수도 있음
border-color
border-width
border-style</p>
</blockquote>
<h3 id="6-박스모델-1편-박스모델-소개">6. 박스모델 1편, 박스모델 소개</h3>
<blockquote>
<h4 id="박스모델">박스모델</h4>
<p>브라우저가 요소를 렌더링 할 때, 각각의 요소는 기본적으로 사각형 형태로 영역을 차지하게 된다. 이 영역을 '박스'라 표현하며, CSS는 박스의 크기, 위치, 속성을 결정할 수 있다. 하나의 박스는 다음 네 개의 영역으로 구성된다.</p>
</blockquote>
<ul>
<li>콘텐츠 영역: width, height</li>
<li>안쪽 여백: padding</li>
<li>경계선(테두리): border-width</li>
<li>바깥쪽 여백: margin</li>
</ul>
<h3 id="7-박스모델-2편-margin-padding-다루기">7. 박스모델 2편, margin padding 다루기</h3>
<blockquote>
<p>여백은 상화좌우 네 개의 면으로 나눈다. 작성자는 각 면의 두께를 개별적으로 정의할 수 있다.</p>
</blockquote>
<blockquote>
<h4 id="여백-조절-방법">여백 조절 방법</h4>
</blockquote>
<ul>
<li>하위 속성 정의하기</li>
<li>여러 값을 한 번에 정의하기</li>
</ul>
<blockquote>
<h4 id="하위속성-정의하기">하위속성 정의하기</h4>
</blockquote>
<pre><code>margin-top: ;
margin-right: ;
margin-bottom: ;
margin-left: ;
padding-top: ;
padding-right: ;
padding-bottom: ;
padding-left: ;</code></pre><blockquote>
<h4 id="여러-값을-한-번에-정의하기">여러 값을 한 번에 정의하기</h4>
</blockquote>
<pre><code>margin: 30px; -&gt; 상하좌우 모두
margin: 30px 10px; -&gt; 상하, 좌우
margin: 30px 10px 10px -&gt; 위, 좌우, 아래
margin: 30px 10px 10px 30px -&gt; 위, 오른쪽, 아래, 왼쪽</code></pre><h3 id="13-flexbox-1편-정의-및-사용-방법">13. flexbox 1편, 정의 및 사용 방법</h3>
<blockquote>
<p>flexbox란?
박스 내 요소 간의 공간 배분과 정렬 기능을 제공하기 위한 1차원 레이아웃 모델이다. flexbox는 flex 컨테이너라고도 한다. flex 컨테이너를 만들기 위해서는 컨테이너에 display:flex; 를 적용해야 한다. flexbox는 자식 요소의 기본 마진값을 무시하고 요소를 배치한다.</p>
</blockquote>
<pre><code>&lt;!DOCTYPE html&gt;
&lt;html lang=&quot;en&quot;&gt;
&lt;head&gt;
    &lt;meta charset=&quot;UTF-8&quot;&gt;
    &lt;title&gt;HTML &amp; CSS 챌린지 5일차&lt;/title&gt;
    &lt;style&gt;
        .container{display: flex;}
        .item{
            width:80px; height: 80px;
            background-color: orange;
        }
    &lt;/style&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;div class=&quot;container&quot;&gt;
        &lt;div class=&quot;item&quot;&gt;1&lt;/div&gt;
        &lt;div class=&quot;item&quot;&gt;2&lt;/div&gt;
        &lt;div class=&quot;item&quot;&gt;3&lt;/div&gt;
    &lt;/div&gt;

&lt;/body&gt;
&lt;/html&gt;</code></pre><blockquote>
<p>flexbox에는 주축과 교차축이 있다.(행, 열 사용자가 선택)
flex-direction 속성을 이용해서 진행 방향을 정할 수 있다.</p>
</blockquote>
<ul>
<li>row</li>
<li>column</li>
<li>row-reverse</li>
</ul>
<pre><code>&lt;!DOCTYPE html&gt;
&lt;html lang=&quot;en&quot;&gt;
&lt;head&gt;
    &lt;meta charset=&quot;UTF-8&quot;&gt;
    &lt;title&gt;HTML &amp; CSS 챌린지 5일차&lt;/title&gt;
    &lt;style&gt;
        .container{
            display: flex;
            flex-direction: column;
        }
        .item{
            width:80px; height: 80px;
            background-color: orange;
        }
    &lt;/style&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;div class=&quot;container&quot;&gt;
        &lt;div class=&quot;item&quot;&gt;1&lt;/div&gt;
        &lt;div class=&quot;item&quot;&gt;2&lt;/div&gt;
        &lt;div class=&quot;item&quot;&gt;3&lt;/div&gt;
    &lt;/div&gt;

&lt;/body&gt;
&lt;/html&gt;</code></pre><p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/fbe39263-cca4-49f3-819f-3a0f368ad49f/image.png" /></p>
<h3 id="14-flexbox-2편-몇-가지-관련-속성">14. flexbox 2편, 몇 가지 관련 속성</h3>
<p>flexbox에는 주축과 교차축의 개념이 중요하다.
주축과 교차축을 기준으로 요소를 배치할 수 있다.</p>
<blockquote>
<h4 id="요소-배치-방법">요소 배치 방법</h4>
</blockquote>
<ul>
<li>주축 배치 방법: justify-content</li>
<li>교차축 배치 방법: align-items</li>
<li>교차축 개별요소 배치 방법: align-self</li>
<li>줄 바꿈 여부: flex-wrap</li>
</ul>
<blockquote>
<h4 id="justify-content-flex-컨텐츠의-주축에서-어떤식으로-정렬을-할지-선택한다">justify-content: flex 컨텐츠의 주축에서 어떤식으로 정렬을 할지 선택한다.</h4>
</blockquote>
<ul>
<li>center: 주축의 가운데</li>
<li>flex-start: flex의 시작부분에</li>
<li>flex-end: flex의 끝부분에</li>
<li>space-around: 균등하게 벌리겠다라는 의미</li>
<li>space-between: 첫 번째, 마지막 요소를 끝에 붙이고 나머지를 균등하게</li>
</ul>
<blockquote>
<h4 id="align-items-교차축-정렬">align-items 교차축 정렬</h4>
</blockquote>
<ul>
<li>flex-end</li>
<li>flex-start</li>
<li>center</li>
</ul>
<blockquote>
<h4 id="align-self-개별요소-하나에만-적용-시키기---클래스를-불러서-가능하다">align-self 개별요소 하나에만 적용 시키기 -&gt; 클래스를 불러서 가능하다.</h4>
<p>flex-start
flex-end</p>
</blockquote>
<blockquote>
<h4 id="flex-wrap-flex컨테이너에서-자식요소가-부모보다-커지면-줄여버림">flex-wrap flex컨테이너에서 자식요소가 부모보다 커지면 줄여버림</h4>
<p>원하지 않는다? flex-wrap: wrap; 두 행 이상으로 처리한다.</p>
</blockquote>
<ul>
<li>wrap-revse 반대로(데칼코마니)</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/76da21d9-74e1-43ba-85f2-0da1bf2d720d/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/d6c4e554-c8a3-4114-8e21-0a6c5f887137/image.png" /></p>
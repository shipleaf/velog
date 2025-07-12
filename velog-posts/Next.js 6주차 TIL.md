<h3 id="1-vercel로-배포하기">1. vercel로 배포하기</h3>
<p>vercel 을 통해 배포하면 https 프로토콜 사용가능하다.</p>
<blockquote>
</blockquote>
<ul>
<li>vercel을 통해 배포</li>
<li>네이버, 구글 서치엔진에 등록</li>
<li>구글 태그매니저 스크립트를 통해 구글 에넬리틱스 추가 가능</li>
</ul>
<ol>
<li><p>Github repository 생성</p>
</li>
<li><p>git 명령어로 작성 코드 업로드</p>
</li>
<li><p>vercel.com 접속</p>
</li>
<li><p>add new project 권한 부여(레퍼지토리 엑세스)</p>
</li>
<li><p>vercel로 import </p>
</li>
<li><p>deploy로 배포 시작</p>
</li>
</ol>
<h3 id="2-네이버-서치-어드바이저에-사이트-등록하기">2. 네이버 서치 어드바이저에 사이트 등록하기</h3>
<p>vercel 도메인탭에서 할당된 도메인 확인 가능하다. 네이버 검색엔진에서 찾으려면 사이트를 네이버 클라우드 폼에 등록해야한다.</p>
<p>카카오 공유 디버거 - oG 프로토콜 디버그
-&gt; og title, 설명 등을 미리 확인할 수 있다.</p>
<h4 id="네이버-서치-어드바이저에-사이트-추가">네이버 서치 어드바이저에 사이트 추가</h4>
<ol>
<li><p>웹 마스터 도구에서 사이트 등록</p>
</li>
<li><p>URL 입력</p>
</li>
<li><p>사이트 소유 확인</p>
</li>
</ol>
<ul>
<li>html 파일 업로드로 확인</li>
<li>meta 태그로 확인
위 두가지 방법으로 사이트 소유를 인증해야 한다.</li>
</ul>
<ol start="4">
<li>sitemap.xml과 robots.txt 파일을 제출</li>
</ol>
<p>웹 사이트 크롤링을 요청하려면 sitemap.xml과 robots.txt 파일을 제출해야 한다. next-sitemap이라는 패키지를 이용해서 쉽게 만들 수 있다.</p>
<ul>
<li>robots.txt는 크롤러에게 어떻게 크롤링 해야하는지 알려주는 파일</li>
<li>sitemap.xml을 사이트에 대한 전체적인 설계를 제시한다.</li>
</ul>
<h3 id="3-구글-서치-콘솔에-사이트-등록하기">3. 구글 서치 콘솔에 사이트 등록하기</h3>
<p>우리는 vercel.app의 소유자가 아니라, <a href="https://inflearn-nextjs.vercel.app%EC%9D%B4%EB%9D%BC%EB%8A%94">https://inflearn-nextjs.vercel.app이라는</a> 웹을 만든 것이기 때문에 구글 서치 콘솔의 URL 접두어를 이용한다.</p>
<ol>
<li><p>소유권 확인: next-seo로 확인 seo.config.hs에 meta태그를 추가</p>
</li>
<li><p>sitemap파일과 robots.txt 추가</p>
</li>
<li><p>URL 검사를통해 사이트 확인 가능 - 색인 생성 요청(크롤링 요청)</p>
</li>
</ol>
<h3 id="4-구글-에널리틱스-스크립트-추가하기">4. 구글 에널리틱스 스크립트 추가하기</h3>
<p>구글 에널리틱스를 사용하면 어떤 페이지에 접속했는지, 어떤 국가에서 접속했는지 등 다양한 유저 정보를 트래킹 가능하다.</p>
<ol>
<li><p>account 계정을 만들고 하위에 사이트 속성을 추가</p>
</li>
<li><p>왼쪽 하단 admin 계정과 속성 추가</p>
</li>
<li><p>플랫폼 웹 선택, 사이트 url 원하는 이름 입력 -&gt; create</p>
</li>
<li><p>googletagmanager스크립트를 파일에 추가: 모든 페이지에 적용되는 App 파일에 스크립트 - next/script</p>
</li>
</ol>
<p>-&gt; googletagmanager을 모든 페이지에서 확인할 수 있음</p>
<p>작은 사이트에서도 구글 에널리틱스를 달아서 출시하는 것을 권장한다.</p>
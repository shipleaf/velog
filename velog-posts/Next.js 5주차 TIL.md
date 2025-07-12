<h2 id="매장-상세-페이지-만들기">매장 상세 페이지 만들기</h2>
<h3 id="1-detailsection-placeholder-ui-구현하기">1. DetailSection placeholder UI 구현하기</h3>
<ul>
<li>상세보기 UI</li>
<li>좌측 하단 네이버 로고 옮기기</li>
</ul>
<h4 id="상세보기-ui">상세보기 UI</h4>
<p>Html:
섹션 구성은 화면을 꽉 채우는 DetailSection에 헤더, 페이지를 접을 수 있는 버튼 그리고 placeholder문구로 구성한다.</p>
<p>Scss:
absolute를 적용하기 위해 main태그에 relative 특성을 추가, DetailSection이 접힌 상태일때 화면 하단에 접힌 페이지가 출력되어야 하므로 transform-translateY를 이용하여 화면 하단으로 페이지를 이동시킨다.</p>
<h4 id="네이버-로고-위치-조정">네이버 로고 위치 조정</h4>
<p>네이버 로고 위치를 매장 상세 페이지의 높이만큼 올려야 노출이 된다. @use를 이용하여 scss파일에서 변수에 접근할 수 있다. bottom 값을 기존의 0에서 header-height + header-padding으로 바꾼다.</p>
<h3 id="2-detailsection-애니메이션-구현하기">2. DetailSection 애니메이션 구현하기</h3>
<ul>
<li>current store name 표시하기</li>
<li>DetailSection 페이지 expand, 토글 표시 변경</li>
</ul>
<h4 id="current-store-name-표시하기">current store name 표시하기</h4>
<p>useSWR과 CURRENT_STORE_KEY로 매장 이름을 가져와서 현재 스토어가 있다면 매장 이름을 표시하고, 없다면 placeholder를 표시한다.</p>
<h4 id="detailsection-페이지-expand-토글-표시-변경">DetailSection 페이지 expand, 토글 표시 변경</h4>
<p>매장이 선택되면 translateY를 -160px로 주고, 토글을 클릭하여 확장하면 0으로 변경, 전체가 노출되도록 변경한다. 기본화면에서 DetailSection이 스크롤되는 현상은 overflow: hidden으로 해결한다.</p>
<p>추가로 expand되었을때 rotate와 bounce를 이용하여 버튼이 180도 바뀌고, 위아래로 진동하도록 스타일을 입힌다.</p>
<h3 id="3-detailsection-ui-완성하기">3. DetailSection UI 완성하기</h3>
<ul>
<li>매장 상세 UI 추가</li>
</ul>
<h4 id="매장-상세-ui-추가">매장 상세 UI 추가</h4>
<p>네이버 이미지를 사용해야 하기 때문에 next.config.js에 도메인을 추가한다. current store가 있다면 정보를 노출하고, 없다면 NULL을 반환한다. 이때, 이미지의 사이즈를 미리 알 수 없기 때문에, 미리 120, 80px로 지정하고, object-fit: cover를 이용하여 비율이 깨지지 않도록 조정한다.</p>
<h3 id="4-getstaticpaths로-각-매장의-상세-페이지-만들기">4. getStaticPaths로 각 매장의 상세 페이지 만들기</h3>
<p>먼저, 페이지를 작성해두고 어떤 값이 후보로 올 수 있는지 제시한다(getStaticPaths 함수 이용). getStaticPaths는 반드시 getStaticProps와 함께 사용한다.</p>
<p>map 함수를 사용하여 stores.json에 있는 모든 매장 정보에 대해 경로를 만들어준다.</p>
<p>getStaticPaths는 페이지의 경로를 미리 정적으로 생성해두고 프리렌더링한다.
fallback 속성에 대해 false라면 404 페이지를 노출하고, true라면 바로 404 페이지를 노출하는 것이 아니라 getStaticProps를 호출한다. blocking은 true와 달리 getStaticProps가 종료될때까지 멈춰있는다.</p>
<h3 id="5-상세-페이지-ui-구현하기">5. 상세 페이지 UI 구현하기</h3>
<p>위에서 작성한 내용으로 매장 상세 페이지를 따로 구현한다.</p>
<h3 id="6-매장-url-공유-기능-구현하기">6. 매장 URL 공유 기능 구현하기</h3>
<ul>
<li>화면 URL을 복사하여 링크 공유</li>
<li>링크를 누르면 해당 매장이 중앙에 위치하도록 랜딩 페이지 이동</li>
</ul>
<h3 id="7-lighthouse로-웹-성능-검사-및-개선하기">7. lighthouse로 웹 성능 검사 및 개선하기</h3>
<p>개발자도구 -&gt; lighthouse를 통해 웹 성능 검사를 실시할 수 있다.
개발 환경을 종료하고 production 환경에서 검사해야 한다.</p>
<p>개선 내용:</p>
<ul>
<li>Large Contentful paint를 warning을 통해 개선</li>
<li>웹접근성 개선</li>
<li>Best Practices는 배포하면서 자연스럽게 개선된다.</li>
<li>SEO</li>
</ul>
<h4 id="large-contentful-paint">Large Contentful paint</h4>
<p>이미지가 크게 요청되면 console창에 warning 표시가 나온다. 이때, width값을 미리 지정해두어 네트워크에서 작은 이미지 파일을 불러올 수 있도록 개선하면 warn 문구가 사라진다.</p>
<h3 id="8-웹접근성-개선하기">8. 웹접근성 개선하기</h3>
<p>공유하기 버튼과 토글 버튼에 적절한 이름이 없으면 스크린리더 사용자에게 좋지 않은 경험을 제공할 수 있다(코드가 어떤 역할을 하는지 정확히 알 수 없다).</p>
<p>aria-label을 이용하여 해당 태그에 라벨을 추가할 수 있다.</p>
<h3 id="9-seo-개선하기feat-next-seo">9. SEO 개선하기(feat. next-seo)</h3>
<ul>
<li>문서에 title이 없다.</li>
<li>description meta tag가 없다.</li>
</ul>
<p>_document 태그를 사용하여 문서의 head 태그에 title을 설정할 수 있다. 하지만, 전역 html문서에 대해 적용하기 때문에 title이 바뀌는 웹에서는 적절하지 않다. 그래서 각각의 페이지마다 next/head를 import하여 title을 작성하는 것이 좋다.</p>
<p>SEO관련 라이브러리를 사용하여 위 방법 사용시 코드 복잡도를 개선할 수 있다.</p>
<p>yarn add next-seo로 패키지를 설치한다.
Next/SEO로 title과 description을 입력하면 자동으로 og: title, og: description을 생성해준다.</p>
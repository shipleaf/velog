<h3 id="1-완성된-header-ui-미리보기">1. 완성된 Header UI 미리보기</h3>
<p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/ac5989a1-5036-46d5-ba6a-58f18720bf35/image.png" /></p>
<ul>
<li>next/link를 통해 페이지 이동</li>
<li>next/image API를 이용해서 인프런 이미지 불러오기</li>
<li>스타일을 입히기 위해 scss 사용</li>
</ul>
<h3 id="2-header-컴포넌트-작성하기">2. Header 컴포넌트 작성하기</h3>
<pre><code>import React from &quot;react&quot;;
import Link from &quot;next/link&quot;;
import styles from '@/styles/header.module.scss';

interface Props {
    rightElements?: React.ReactElement[];
}

const HeaderComponent = ({ rightElements } : Props) =&gt; {
    return (
        &lt;header className = {styles.header}&gt;
            &lt;div className = {styles.flexItem}&gt;
                &lt;Link href=&quot;/&quot; className = {styles.box}&gt;
                    &lt;img 
                        src=&quot;/inflearn.png&quot;
                        width={110}
                        height={20}
                        alt=&quot;인프런 로고&quot;
                    /&gt;
                &lt;/Link&gt;
            &lt;/div&gt;
        &lt;/header&gt;
    );
};


export default HeaderComponent</code></pre><p>img 태그를 이용하여 외부 이미지를 다운로드 후 렌더링하는 방식</p>
<p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/44be1967-220e-4671-a359-d01f71c5b7b9/image.png" /></p>
<pre><code>yarn add sass</code></pre><p>위의 명령어를 통해 sass 설치</p>
<pre><code>.header {
    position: absolute; // 로고가 상단에 위치해야 하기 때문에 absolute로 위치를 잡아줌
    top: 0;
    left: 0;

    width: 100%;
    height: 40px;
    padding: 0 8px 0 12px;

    display: flex;
    justify-content: space-between; // 화면 양쪽에 버튼이 위치하도록
    align-items: center;

    z-index: 100;
    pointer-events: none;   // 화면 가운데는 클릭이 되야함
}

.flexItem {
    display: flex;
    pointer-events: auto;   // click 이벤트가 작동해야하기 때문에
}

.box {
    padding: 6px;
    border: none;
    border-radius: 4px;
    box-shadow: 0 2px 4px 0 rgb(136 136 136 / 30%);

    display: flex;
    align-items: center;
    justify-content: center;

    background-color: #fff;
    &amp;:active {
        background-color: #40a6fd;
        color: white;
    }
    transition: background-color 200mx ease;
    // 클릭시 배경색이 자연스럽게 변하도록 설정
}</code></pre><p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/99ac2ed4-cc56-4d41-a1f0-fb67a7c94c73/image.gif" />
위와 같이 스타일링이 된다.</p>
<p>하지만, 위처럼 html의 img태그를 이용할시 eslint 경고문이 뜨면서 next/image의 옵션을 사용할 수 없다.</p>
<h3 id="3-nextimage">3. next/image</h3>
<h4 id="image-렌더링-방식">image 렌더링 방식</h4>
<p>1) image 태그에서 이미지 파일을 static하게 import</p>
<pre><code>import example from '/public/example.jpg';

      &lt;figure&gt;
        &lt;Image
          src={example}
          alt=&quot;v13 image&quot;
          width={500}
          height={100}
          placeholder=&quot;blur&quot;
         /&gt;
        &lt;figcaption&gt;v13 image&lt;/figcaption&gt;
        &lt;/figure&gt;</code></pre><p>2) 외부에서 링크 가져오기</p>
<pre><code>&lt;figure&gt;
        &lt;Image
          src=&quot;https://inflearn-nextjs.vercel.app/example.jpg&quot;
          alt=&quot;v13 image&quot;
        /&gt;
        &lt;figcaption&gt;v13 image&lt;/figcaption&gt;
      &lt;/figure&gt;</code></pre><p>위의 방식으로 작성하면 에러 발생, 크기를 지정해줘야함.</p>
<pre><code>width={500}
height={100}    // 코드 추가</code></pre><h4 id="nextimage의-장점">next/image의 장점</h4>
<ol>
<li><p>이미지 용량 최적화
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/656bf7c1-9d6a-4ffb-bbc3-f9a0a0632ab0/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/9462f68f-9f5f-4642-aed3-51771a5daa5c/image.png" />
이미지 파일을 webp 형식으로 불러와 용량 최적화를 할 수 있다.</p>
</li>
<li><p>lazy 로딩 자동 적용
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/bfcb7b5f-e2bc-4a6f-9691-790a5fed78e2/image.gif" />
이미지 파일이 있는 위치에 접근할때 lazy하게 네트워크를 다운로드하는 lazy 로딩을 자동으로 제공한다.</p>
</li>
<li><p>placholder = &quot;blur&quot;
blur 명령어를 통해 사진을 불러오는 동안 자동으로 블러처리를 도와준다.</p>
</li>
</ol>
<p>만약, 외부 이미지를 불러올때 크기를 알 수 없을때는 fill 속성을 이용한다. fill 속성은 부모의 크기에 맞춰 이미지의 크기를 조정한다.</p>
<pre><code>&lt;figure style={{ position: 'relative', width: '500px', height: '100px' }}&gt;    // 부모 태그의 크기 조정
fill</code></pre><p>이전 버전의 next/legacy/image API는 img 태그 생성시 레이아웃을 스타일링 하기 위해 span 태그를 생성한다. next/image는 이러한 네트워크의 비효율성을 줄이기 위해 업데이트 되었다.</p>
<h3 id="4-header-컴포넌트-완성하기">4. Header 컴포넌트 완성하기</h3>
<h4 id="header-컴포넌트">Header 컴포넌트</h4>
<pre><code>import React from &quot;react&quot;;
import Link from &quot;next/link&quot;;
import styles from '@/styles/header.module.scss';
import Image from &quot;next/image&quot;;

interface Props {
    rightElements?: React.ReactElement[];    //rightElements Props 추가
}

const HeaderComponent = ({ rightElements } : Props) =&gt; {
    return (
        &lt;header className = {styles.header}&gt;
            &lt;div className = {styles.flexItem}&gt;
                &lt;Link href=&quot;/&quot; className = {styles.box}&gt;
                    &lt;Image 
                        src=&quot;/inflearn.png&quot;
                        width={110}
                        height={20}
                        alt=&quot;인프런 로고&quot;
                    /&gt;
                &lt;/Link&gt;
            &lt;/div&gt;
            {rightElements &amp;&amp; &lt;div className={styles.flexItem}&gt;{rightElements}&lt;/div&gt;}    // logo 우측에 div 추가
        &lt;/header&gt;
    );
};


export default HeaderComponent;</code></pre><h4 id="indextsx">index.tsx</h4>
<pre><code>import { Fragment } from &quot;react&quot;;
import Header from '@/components/common/Header';
import styles from '@/styles/header.module.scss';
import Link from &quot;next/link&quot;;
import { AiOutlineShareAlt } from &quot;react-icons/ai&quot;; // next-icon 설치 후 마음에 드는(?) 아이콘 선택
import { VscFeedback } from &quot;react-icons/vsc&quot;;

export default function Home() {
  return (
    &lt;Fragment&gt;
      &lt;Header rightElements={[
        &lt;button 
          onClick={() =&gt; {    // 클릭 이벤트 발생시 '복사!' 텍스트 출력
            alert('복사!');
          }}
          className={styles.box}
          style={{marginRight: 8}}
          key=&quot;button&quot;
        &gt;
          &lt;AiOutlineShareAlt size={20} /&gt;
        &lt;/button&gt;,
        &lt;Link href=&quot;/feedback&quot; className={styles.box} key=&quot;Link&quot;&gt;
          &lt;VscFeedback size={20} /&gt;
        &lt;/Link&gt;
      ]}
      /&gt;

      &lt;main&gt;&lt;/main&gt;
    &lt;/Fragment&gt;
  );
}</code></pre><p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/e2d95fe5-4866-406f-aed1-771084d88e39/image.gif" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/b9c7e562-ed30-49e6-99fa-f62a5b1f3c31/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/77636d6a-de63-4edc-bcda-b03cb5576204/image.png" /></p>
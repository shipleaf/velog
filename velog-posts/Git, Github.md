<blockquote>
<p>Github란?
프로젝트 코드가 로컬 컴퓨터에만 저장되어 있기 때문에 코드 저장 및 동료들에게 공유하기 좋은 도구입니다. 즉, 코딩 외 실무적인 문제를 해결해주는 도구입니다.</p>
</blockquote>
<blockquote>
<p>Github의 역할</p>
</blockquote>
<ol>
<li>내 소스코드를 저장(버전관리)</li>
<li>소스코드를 공유</li>
<li>협업하는 공간</li>
</ol>
<p>Github는 소스코드를 올리는 공간, Git은 내 컴퓨터에서 인터넷으로 올려주는 역할을 합니다.</p>
<ol>
<li><p>Git 설치
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/7ef61cec-13e4-47e8-b408-66db5acc8916/image.png" />
<a href="https://git-scm.com/">https://git-scm.com/</a></p>
</li>
<li><p>Git bash 환경설정</p>
<blockquote>
<p>Git bash를 사용하는 이유?
Git bash를 사용하여 우리가 사용하는 운영체제인 window 운영체제 환경에서도 리눅스 명령어를 사용할 수 있게 된다.</p>
</blockquote>
</li>
</ol>
<pre><code>git config --global user.name &quot;shipleaf&quot; // 사용자 이름 설정
git config --global user.email &quot;sunyeop12@gmail.com&quot; // github에 사용한 이메일

git config --list // 확인</code></pre><p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/983ce5ec-b7ec-4452-8907-c59b1c2042af/image.png" /></p>
<pre><code>git init // git 작업공간을 기준으로 git 저장소 생성
git add . // .은 파일 전부를 의미, 변경내용을 저장
git status // git add에 대한 변경내용을 확인</code></pre><p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/29f3e7d1-236e-4e8f-8ed1-df704f5a30b2/image.png" /></p>
<pre><code>git commit -m &quot;first commit&quot; // add와의 차이, 히스토리 생성</code></pre><p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/32de1734-51ef-46bb-a1f7-1f5aa73b787d/image.png" />
 commit으로 생성한 히스토리를 github로 보내기 위해서는 레퍼지토리의 주소가 필요합니다.
 <img alt="" src="https://velog.velcdn.com/images/shipleaf/post/3499634b-edc3-4c8b-a395-1350f83282d6/image.png" /></p>
<pre><code>git remote add origin 레퍼지토리주소
git remote -v // 주소 연결 확인</code></pre><p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/69e422c6-ac4e-4294-9c54-3c946c871cca/image.png" /></p>
<pre><code>git push origin master</code></pre><pre><code class="language-The">ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])?</code></pre>
<p>GitHub에 올라간 Repository를 아무나 pull 또는 push를 하게 되면 큰 문제가 생길 수 있습니다. 때문에 해당 기능을 사용하기 위해선 유저에게 권한이 있는지 확인이 필요한데, 이때 필요한 것이 publickey입니다. 해당 PC에서 생성된 키가 GitHub 계정에 등록된 경우에만 해당 기능을 사용할 수 있습니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/44c5d7a3-3c62-4030-8c31-03320049b870/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/cbedd64d-4ab1-453b-9c34-3e1ccaee0555/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/b94139ae-c256-4896-b9e3-26e65e1ab1d2/image.png" /></p>
<h3 id="github-소스코드-가져오기">Github 소스코드 가져오기</h3>
<p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/233dec46-7ad7-4458-8a6a-192f3d2be458/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/690ee39f-bc71-4c58-9787-57e7e26e5045/image.png" /></p>
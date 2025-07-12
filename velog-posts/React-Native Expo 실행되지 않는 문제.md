<p><img align="center" alt="example" height="200" src="https://velog.velcdn.com/images/shipleaf/post/6301c374-7200-4087-93f3-8a1a86866050/image.png" width="200" /></p>
<h2 id="문제">문제</h2>
<p>React-Native Expo를 에뮬레이터에서 실행했을 때는 잘 되지만, 휴대폰을 연결하면 위 사진처럼 오류가 발생했다. 찾아보니 같은 네트워크에 연결되지 않으면 발생할 수 있는 문제라고 하는데, pc와 휴대폰 모두 같은 네트워크에 연결되어 있었다.</p>
<h2 id="해결">해결</h2>
<p>나는 expo 앱 실행을 카페 공용 와이파이를 이용해서 실행했는데 이렇게 하면 공용 와이파이가 LAN 접속을 차단하는 문제가 있거나, 개인 pc의 방화벽이 실행을 막는 경우가 생긴다고 한다.</p>
<p>따라서, Expo를 tunnel 모드로 실행하면 해결된다. Tunnel 모드는 같은 네트워크일 필요 없이 인터넷으로 동작하기 방화벽 문제등을 우회할 수 있다(속도가 조금 떨어지는 부작용은 있음!).</p>
<br />

<pre><code>expo start --tunnel</code></pre>
<h2 id="typescript">Typescript</h2>
<blockquote>
<p>JavaScript 기반의 정적 타입 문법을 추가한 언어</p>
</blockquote>
<ul>
<li>장점: 컴파일 과정에서 타입이 지정되어 있기 때문에 에러를 예방, 손쉬운 디버깅이 가능하다</li>
</ul>
<h3 id="1-설치">1. 설치</h3>
<pre><code>npm install -g typescript</code></pre><h3 id="2-변수">2. 변수</h3>
<p>변수는 이름과 공간을 담는다. Javascript와의 차이는 '타입'을 지정한다는 것이다.</p>
<pre><code>var isDone: boolean = false;
var isDone: any = 1234;        // 변수 타입을 any로 지정하면 타입에 상관없이 지정가능</code></pre><blockquote>
<h4 id="null-vs-undefined">null vs undefined</h4>
<p>null은 빈 값을 표현하는 '값'이고, undefined는 값이 지정이 안된 상태를 말한다.</p>
</blockquote>
<pre><code>### 리스트 변수 지정
var list: number[] = [1,2,3];
var list: Array&lt;number&gt; = [1,2,3];</code></pre><h3 id="3-함수">3. 함수</h3>
<p>함수도 변수와 마찬가지로 argument의 타입을 지정해준다.</p>
<pre><code>function sayHello(name: string){
    ....
}
sayHello(&quot;shipleaf&quot;)</code></pre><h3 id="4-오브젝트">4. 오브젝트</h3>
<p>Python의 dict와 유사한 구조를 가진다.</p>
<pre><code>var object = {
    firstName: &quot;John&quot;,    - ㅡmember 혹은 property라 부른다.
    secondName: &quot;...&quot;
}</code></pre><h3 id="5-인터페이스">5. 인터페이스</h3>
<p>자료 구조나 함수의 구조에 대한 약속이다.</p>
<pre><code>변수의 타입을 지정
Interface Person{
    name: string;
    age?: number;    # ?의 의미는 인터페이스를 사용할때 필수로 포함하지 않아도 된다는 의미
    move(): void;
}</code></pre><h3 id="6-클래스">6. 클래스</h3>
<p>클래스는 실제 세계의 물체를 표현(정보와 행동), 인터페이스와는 구분된 특징을 가진다.</p>
<ul>
<li>constructor</li>
<li>함수의 내용(행동)</li>
</ul>
<pre><code>class Point{
    x: number
    constructor(x :number, public y: number) {
        this.x = x;
    }
    dist(){
        return ...
    }
    static origin = new Point(0, 0);
}

var point1 = new Point(0, 0) # class 활용</code></pre>
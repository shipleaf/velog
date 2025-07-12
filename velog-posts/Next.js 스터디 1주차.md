<h2 id="typescript">Typescript</h2>
<p>Typescript란 Javascript에서 변수 타입 지정, 객체 지향 프로그래밍 등의 특징을 추가한 언어이다.</p>
<h3 id="typescript-관련-간단-명령어">Typescript 관련 간단 명령어</h3>
<h4 id="--typescript-설치">- Typescript 설치</h4>
<pre><code>npm install -g typescript</code></pre><p>위 명령어를 터미널에 입력하여 설치한다.</p>
<h4 id="--typescript-버전-확인">- Typescript 버전 확인</h4>
<p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/8aabeafd-d278-4bd0-8b48-2835f041ed79/image.png" /></p>
<pre><code>tsc -v</code></pre><p>tsc -v 명령어를 통해 Typescript의 버전을 확인한다.</p>
<h4 id="--typescript-파일을-javascript-파일로-변환">- Typescript 파일을 Javascript 파일로 변환</h4>
<p>Typescript 파일을 실행하기 위해서는 Javascript 파일로 컴파일한 후 변환한 Javascript 파일을 실행하는 방법을 사용한다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/e655ca43-f021-46d6-8d1a-8faac13aef2c/image.png" />
위와 같은 hello.ts Typesciprt 파일을</p>
<p>tsc hello.ts 명령어를 이용하여 아래 사진과 같은 Javascript파일로 변환할 수 있다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/e7a8d467-6a57-4f68-b1d8-e2de1ef04892/image.png" /></p>
<h3 id="typescript-코드-테스트">Typescript 코드 테스트</h3>
<p>Typescrpt 코드를 테스트하는 두 가지 방법이 있다. 하나는 웹브라우저에서 직접확인 하는 방법이고, 다른 하나는 Typescript playground에서 확인하는 방법이다.</p>
<h4 id="웹-브라우저로-확인">웹 브라우저로 확인</h4>
<pre><code>alert('hello world from typescript');
console.log('hello world');</code></pre><p>위 코드를 js로 변환 후 html 문서에 적용하고 브라우저를 열어 확인한다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/903c778f-c66f-4674-955f-b1281a38e1aa/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/7ca12248-bb02-4cbd-8bce-0f08c7cc59cb/image.png" /></p>
<h4 id="typescript-playground에서-확인">Typescript playground에서 확인</h4>
<p>Typescript Playground 웹사이트에서 코드를 붙여넣고 실행시켜 확인한다.
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/b10d5bdc-e539-4226-b979-584e010ba7c0/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/e3b6bed0-0439-455a-b9b1-6e4db8b1f584/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/510ce8b9-9460-41c5-aefa-9dcfc491535e/image.png" /></p>
<h3 id="typescript-변수">Typescript 변수</h3>
<p>변수는 값을 저장하는 공간을 의미하며, 역할과 의미를 부여해서 선언한다.
Typescript에서는 </p>
<pre><code>var 변수명: 타입 = 값;</code></pre><p> 의 방식으로 변수를 선언한다.</p>
<ul>
<li><p>Javascript 변수 선언 방식</p>
<pre><code>var number = 10;
var string = &quot;Hello&quot;;
var list = [1, 2, 3, 4, 5];
var boolean = True;</code></pre></li>
<li><p>Typescript 변수 선언 방식</p>
<pre><code>var number: number = 10;
var string: string = &quot;Hello&quot;;
var list: number[] = [1, 2, 3];
var list: Array &lt;number&gt; = [1, 2, 3];
var boolean: boolean = True;

var variable: any = 10;    // 변수의 타입을 확신할 수 없을 때 any type을 사용한다.</code></pre><p>Typescript에서는 null과 undefined를 제공한다. 
- null은 변수가 비어있다는 것을 명시하는 '값'이다.
- undefined는 변수가 비어있다는 명시조차 되지 않은 것이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/shipleaf/post/eb1b4a45-13da-4418-b15f-4c6c15f7a8f6/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/f99073b3-2372-4f9a-b95f-97efe66007c5/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/587b70a1-8582-4fed-823d-083dd6c39aff/image.png" />
<img alt="" src="https://velog.velcdn.com/images/shipleaf/post/fe666b0f-47e8-48f7-9fed-e73d73c409ea/image.png" /></p>
</li>
</ul>
<h3 id="typescript-함수">Typescript 함수</h3>
<h4 id="typescript-함수-호출">Typescript 함수 호출</h4>
<p>Typescript의 함수 호출 방식은 Javascipr와 유사하지만, 변수 선언과 마찬가지로 인자의 type을 설정해줘야 한다.</p>
<ul>
<li>Javascript 함수 선언<pre><code>function sayHello(name) {
  alert('hello ' + name);
}
sayHello('shipleaf');</code></pre></li>
<li>Typescript 함수 선언<pre><code>function sayHello(name: string) {
  alert('hello ' + name);
}
sayHello('shipleaf');</code></pre>Typescript 함수를 변수에 저장할 수 있다.
```</li>
</ul>
<ol>
<li>var f1 = function(i: number): number {return i * i;}</li>
<li>var f2 = function(i: number) {return i * i;}</li>
<li>var f3 = (i: number): number =&gt; {return i*i;}</li>
<li>var f4 = (i: number) =&gt; {return i * i;}</li>
<li>var f5 = (i: number) =&gt; i * i;<pre><code></code></pre></li>
</ol>
<h3 id="typescript-조건문">Typescript 조건문</h3>
<p>Typescript의 조건문은 Javascript와 유사하다.</p>
<ul>
<li>if 문<pre><code>var homeworkDone: boolean = True;
if (homeworkDone == True){
  console.log('Then you can play now');
} else {
  console.log('You have to do homework');
}</code></pre></li>
<li>switch 문<pre><code>var score: string = 'C';
</code></pre></li>
</ul>
<p>switch (score) {
    case 'A':
        console.log('You got an A');
        break;
    case 'B':
        console.log('You got an B');
        break;
    case 'C':
        console.log('You got an C');
        break;
    default:
        console.log('You didn't get any score');
        break;
 }</p>
<pre><code>
 ### Typescript 반복문
 - for문</code></pre><p> var i;
 for (i = 0; i &lt; 3; i++) {
     console.log(i);
 }</p>
<pre><code> - while문
 while문은 조건문이 참일 경우에만 반복되며, 무한루프에 빠지지 않도록 break문이나 변수 차감식을 이용하여 반복에 제한을 둬야한다.</code></pre><p> var i: number = 10;</p>
<p> while(i &gt; 0){
     console.log(i + 'left');
    i -= 1;
 }</p>
<p> var i: number = 10;</p>
<p> while(True){
     console.log('hello');
    i -= 1;
    if(i == 0) {
        break;
    }
 }</p>
<pre><code> +) continue문은 반복문에 사용되며, 해당 사이클의 이후 코드를 무시하고 다음 반복문을 실행한다.

 ### Typescript Object
 Javascript와 Typescript에서의 오브젝트는 Python의 오브젝트와는 느낌이 다르다. 오히려 Python의 dictionary 개념과 유사하다. 여러 변수(혹은 함수)가 하나로 구조화된 상태를 말한다. Typescript의 오브젝트는 javascript와 유사하다.
 예시)</code></pre><p> var personObject = {
     fistName : &quot;John&quot;;
    lastName : &quot;Smith&quot;;
 }</p>
<pre><code> 오브젝트의 변수를 member 혹은 property라고 부른다.
 Typescript의 hasOwnPropery 함수를 사용해서 반복문을 설정할 수 있다.</code></pre><p> var personObject = {
     fistName : &quot;John&quot;;
    lastName : &quot;Smith&quot;;
 }</p>
<p> personObject[&quot;salary&quot;] = 14000;</p>
<p> for (var member in personObject) {
     if (personObject.hasOwnProperty(member){
        console.log(&quot;The member&quot; + member +
        &quot; of personObject is&quot; + personObject[member])
    }
 }</p>
<pre><code>
### Typescript Interfaces
Typescript의 interface는 객체의 구조를 정의하는데 사용한다. Interface는 다음과 같은 방법으로 정의된다.</code></pre><p>interface Person {
    name: string;
    age?: number;
}</p>
<pre><code>위의 예시에서 ?기호가 붙은 변수 age는 선택가능한 변수다. 즉, 입력이 선택사항이다.
예시)</code></pre><p>interface searchFunc{
    (source: string, substring: string): boolean;
}</p>
<p>var mySearch: searchFunc;
mySearch = function(src: string, sub: string){
    return src
}</p>
<pre><code>변수명은 꼭 interface 함수와 같을 필요는 없다.

### Typescript Classes
클래스는 물체의 정보와 함수를 포함하는 도구이다. 인터페이스와는 constructor, 함수 유무등의 차이가 있다.</code></pre><p>class Point {
    x: number;</p>
<pre><code>constructor(x: number, public y:number = 0){ // public을 이용해 y를 선택적으로 받을 수 있다.
    this.x = x; // class의 x = instance의 x
}
dist(){    // interface와 달리 함수에 내용이 꼭 들어가야 한다.
    return Math.sqrt(this.x * this.x + this.y * this.y);
}
static origin = new Point(0,0);</code></pre><p>}</p>
<p>var Point1 = new Point(10,20);
var Point2 = new Point(25);</p>
<pre><code>
### Typescript callback, popup
- callback: argument로 넘길 수 있는 인자로, 원하는 시간이나 조건에 함수를 실행할 수 있도록 설정한다.</code></pre><p>var callback function() {
    alert('콜백 되었습니다.')
}
callback(callback, 3000)    // 1000 = 1sec</p>
<pre><code>
- popup
1. alert
2. prompt
3. confirm

confirm은 ok와 cancel 둘 중 하나를 선택하게 되는데, 이때 ok는 True 값을 cancel은 False 값을 가진다. 따라서 confirm을 if나 while문의 조건식으로 활용할 수 있다.

## 개발 환경 설정
    1. npx create-next-app@latest --typescript
    2. yarn dev // next.js 설치 확인</code></pre><p>yarn: The term 'yarn' is not recognized as a name of a cmdlet, function, script file, or executable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.</p>
<pre><code>    npm install -g yarn

ESLint는 next.js 문법을 교정해주는 도구이고, prettier는 코드를 좀 더 깔끔하게 해주는 formatter이다. 
![](https://velog.velcdn.com/images/shipleaf/post/ce3af677-f581-4b10-8648-5910c7d4df47/image.png)
![](https://velog.velcdn.com/images/shipleaf/post/83d963d7-71e2-4470-8c2a-847fab3353ab/image.png)

next.js 웹 확인을 위해</code></pre><p>export default function Home() {</p>
<p>  return &lt;&gt;Hello World!&lt;/&gt;;
}</p>
<pre><code>index.tsx를 다음과 같이 수정, 아래의 결과가 나온다.

![](https://velog.velcdn.com/images/shipleaf/post/45823afd-faee-48c0-be3f-cd61b6e73549/image.png)
</code></pre>
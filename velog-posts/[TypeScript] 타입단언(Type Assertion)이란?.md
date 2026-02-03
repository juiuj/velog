<h2 id="타입-단언">타입 단언</h2>
<p>타입스크립트에서의 타입 단언이란 개발자가 변수의 타입을 명시적으로 지정할 수 있는 방법.</p>
<p>Q.<span style="color: red;"> 타입단언은 주로 어떨 때 사용될까요?</span>
A. <del><span style="color: gray;"> 컴파일러가 타입을 정확하게 추론하지 못하거나, 개발자가 특정 상황에서 타입을 더 명확하게 전달할 때 사용됨.</span></del></p>
<pre><code class="language-typescript">const a = 'hi' as any;</code></pre>
<p><code>as</code>를 통해 타입단언을 사용할 수 있음.</p>
<p>EX) </p>
<pre><code class="language-typescript">type Person = { name: string; age: number; }

const b = {} as Person;
b.name = 'Thor';</code></pre>
<p>위 코드에서 <code>Person</code>은 <code>{ name: string; age: number; }</code> 형태의 객체를 요구하고 있음.
<code>const b = {} as Person;</code>이 부분에서 실제로는 빈 객체 <code>{}</code>지만 <code>as Person</code>로 이 객체가 <code>Person</code> 타입임을 <strong>단언</strong>하는 과정임.</p>
<h4 id="이와같은-타입-단언은">이와같은 타입 단언은</h4>
<p>타입스크립트 컴파일러에게</p>
<blockquote>
<p>&quot;다음의 값은 이런 타입을 가진거야 그러니까 에러를 띄우지마!&quot;</p>
</blockquote>
<p>라고 말하는 것임.</p>
<hr />
<p>타입 단언 사용을 할 경우엔 오류가 난 코드를 컴파일 단계에서 발견하지 못하고 <code>런타임 단계</code>까지 가야 발견할 수가 있는데 이는 <strong>타입스크립트를 사용하는 장점을 무시한 셈이다...</strong>
(<code>any</code> 타입과 마찬가지로 <code>타입단언</code> 또한 남용해선 안됨)
<img alt="" src="https://velog.velcdn.com/images/dev-joohee/post/75b04735-391f-425f-8571-c43ee3875c7c/image.png" /></p>
<hr />
<p><em>그럼에도 불구하고 <strong>타입단언을 사용하는 이유</strong>는 무엇인가?</em></p>
<h3 id="타입-단언의-효용성이-높은-시점은-언제인가">타입 단언의 효용성이 높은 시점은 언제인가?</h3>
<h4 id="1-html요소에-접근할-때">1. HTML요소에 접근할 때</h4>
<pre><code class="language-typescript">const Modal: React.FC = () =&gt; {
  return (
    &lt;&gt;
      {createPortal(
        &lt;Backdrop /&gt;,
        document.getElementById(&quot;backdrop&quot;) as HTMLDivElement
      )}
      {createPortal(
        &lt;ModalWrapper /&gt;,
        document.getElementById(&quot;overlay&quot;) as HTMLDivElement
      )}
    &lt;/&gt;
  );
};</code></pre>
<p>위의 코드는 react의 createPortal을 이용해서 Modal 컴포넌트를 만든 예시임.</p>
<p>index.html에 미리 <code>&lt;div id=backdrop&gt;</code>과 <code>&lt;div id=overlay/&gt;</code>를 만들어 두고 위와 같이 사용한다면 타입 단언을 사용해야 함.</p>
<h4 id="2-외부-데이터-소스와의-상호작용-시">2. 외부 데이터 소스와의 상호작용 시</h4>
<pre><code class="language-typescript">let data: any = fetchDataFromAPI();
let user = data as User;  // 데이터가 User 타입임을 단언</code></pre>
<p>API 호출이나 외부 라이브러리에서 데이터를 받아올 때 데이터의 타입이 <code>any</code>로 처리되는 경우가 많음. 이때 타입 단언을 사용해서 해당 데이터의 타입을 명확히 지정할 수 있음.</p>
<p>위의 코드에서는 <code>as User</code>를 사용하여 데이터가 <code>User</code> 타입임을 단언하였음</p>
<hr />
<h3 id="타입-단언으로-span-stylecolorred특정-타입을-강제할-수-없는span-상황은">타입 단언으로 <span style="color: red;">특정 타입을 강제할 수 없는</span> 상황은?</h3>
<p>타입스크립트의 타입 단언은 <code>컴파일 타임</code>에만 유효하며 <code>런타임</code>에서 <strong>실제로 타입이 맞는지</strong> 검사하지 않음.</p>
<h4 id="1-호환되지-않는-타입을-강제하는-경우">1. 호환되지 않는 타입을 강제하는 경우</h4>
<pre><code class="language-typescript">let value: any = 42;
let str = value as string;  // 런타임 오류 가능</code></pre>
<p>위의 코드와 같이 숫자를 문자열로 단언하면 <code>컴파일러</code>는 통과시키지만 <code>런타임</code>에서 오류가 발생할 수 있음.</p>
<h4 id="2-null이나-defined에-대한-잘못된-단언">2. null이나 defined에 대한 잘못된 단언</h4>
<p><code>null</code> 인 값을 특정 객체 타입으로 단언하면, <code>런타임</code>에서 <strong>속성에 접근할 때</strong> 오류가 발생할 수 있음.</p>
<pre><code class="language-typescript">let someValue: any = null;
let obj = someValue as { name: string };  // null을 객체로 단언</code></pre>
<h4 id="3-dom-요소가-존재하지-않을-때">3. DOM 요소가 존재하지 않을 때</h4>
<p><strong>DOM 요소가 없는 경우</strong>에도 타입 단언을 하면, <code>속성</code> 접근 시 오류가 발생할 수 있음.</p>
<pre><code class="language-typescript">let inputElement = document.getElementById(&quot;nonExistent&quot;) as HTMLInputElement;
inputElement.value = &quot;Hello&quot;;  // 런타임 오류
</code></pre>
<p>위 코드에서는 <code>nonExistent</code>라는 id를 가진 HTML 요소가 없을 때, <code>null</code>을 입력 필드처럼 사용하려고 해서 오류가 발생할 수 있음.</p>
<h4 id="4-타입-변환과-혼동">4. 타입 변환과 혼동</h4>
<p><strong>타입단언은 값 자체를 변환하진 않음</strong>. 문자열을 숫자로 단언해도 <strong>실제 값은 변하지 않기 때문에</strong> <code>런타임 오류</code>가 발생할 수 있음.</p>
<pre><code class="language-typescript">let str: any = &quot;123&quot;;
let num = str as number;  // 변환되지 않음, 오류 가능</code></pre>
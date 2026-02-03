<h3 id="함수-타입-지정-₩수정하기">함수 타입 지정 <del>₩</del>수정하기</h3>
<blockquote>
<p><span style="color: red;">타입스크립트에서 함수 파라미터에 타입을 지정하는 것은 함수의 인자에 대해 <strong>명확한 타입</strong>을 정의하고 <strong>타입 안정성</strong>을 보장함.
  또한 파라미터에 타입 지정을 통해 함수가 호출될 때 <strong>잘못된 타입의 인자가 전달되는 것을 컴파일 단계에서 방지할 수 있음</strong>.</span></p>
</blockquote>
<h4 id="1️⃣-기본적인-함수-파라미터-타입-지정">1️⃣ 기본적인 함수 파라미터 타입 지정</h4>
<p>: 각 함수의 파라미터에 <code>명시적</code>으로 타입을 지정하여 <strong>함수 호출 시 타입 오류를 방지</strong>함.</p>
<pre><code class="language-typescript">function greet(name: string): void {
  console.log(&quot;Hello, &quot; + name);
}

greet(&quot;Alice&quot;);  // 정상 작동
greet(42);       // 오류 발생: Argument of type 'number' is not assignable to parameter of type 'string'.
</code></pre>
<p>이 코드에서 <code>greet</code> 함수는 <code>name</code>이라는 <strong>문자열(string)</strong> 타입의 파라미터를 받음.
만약 <code>string</code>이 아닌 <code>number</code>나 다른 타입의 값을 전달하면 타입스크립트는 컴파일 시점에서 오류를 발생시킴.</p>
<hr />
<h4 id="2️⃣-여러-파라미터에-타입-지정">2️⃣ 여러 파라미터에 타입 지정</h4>
<p>: 여러 개의 파라미터가 있는 함수에서도 각각의 파라미터에 타입을 지정할 수 있음. 각 파라미터는 함수 정의에서 각자의 타입을 가져야 함.</p>
<pre><code class="language-typescript">function add(a: number, b: number): number {
  return a + b;
}

add(5, 3);     // 정상 작동
add(5, &quot;3&quot;);   // 오류 발생: Argument of type 'string' is not assignable to parameter of type 'number'.
</code></pre>
<p>이 함수는 두 개의 숫자 number 파라미터를 받고 그 합을 반환함.
만약 파라미터 중 하나라도 숫자가 아니면 <strong>컴파일 에러</strong>가 발생함.</p>
<hr />
<h4 id="3️⃣-선택적-파라미터">3️⃣ 선택적 파라미터</h4>
<p>: 타입스크립트에서는 특정 파라미터가 <strong>필수가 아니도록</strong> 할 수 있음. 이를 <code>선택적 파라미터(optional parameter)</code>라고 하며, 파라미터 뒤에 <code>물음표</code>(<code>?</code>)를 붙여서 선언할 수 있음. 선택적 파라미터는 전달되지 않을 경우 <code>undefined</code> 값을 가짐.</p>
<pre><code class="language-typescript">function greet(name: string, age?: number): void {
  if (age) {
    console.log(`Hello, ${name}. You are ${age} years old.`);
  } else {
    console.log(`Hello, ${name}.`);
  }
}

greet(&quot;Alice&quot;);        // &quot;Hello, Alice.&quot;
greet(&quot;Bob&quot;, 25);      // &quot;Hello, Bob. You are 25 years old.&quot;
</code></pre>
<hr />
<h4 id="4️⃣-기본값이-있는-파라미터default-parameter">4️⃣ 기본값이 있는 파라미터(Default Parameter)</h4>
<p>: 파라미터에 <code>기본값</code>을 설정할 수 있음. 설정한 기본값이 있는 파라미터는 함수가 호출될 때 <strong>해당 인자를 전달하지 않으면 기본값</strong> 이 사용됨.</p>
<pre><code class="language-typescript">function greet(name: string, greeting: string = &quot;Hello&quot;): void {
  console.log(greeting + &quot;, &quot; + name);
}

greet(&quot;Alice&quot;);         // &quot;Hello, Alice&quot;
greet(&quot;Bob&quot;, &quot;Hi&quot;);     // &quot;Hi, Bob&quot;
</code></pre>
<p><code>greeting</code> 파라미터는 기본값으로 <code>&quot;hello&quot;</code>를 가지며, 값이 전달되지 않으면 기본값이 사용됨.</p>
<hr />
<h4 id="5️⃣-rest-파라미터rest-parameter">5️⃣ Rest 파라미터(Rest Parameter)</h4>
<p>: <code>Rest</code> 파라미터를 사용하면 함수가 가변 인자를 받을 수 있음. Rest 파라미터는 <code>배열</code>로 수집되며, <code>타입</code> 또한 배열 타입으로 지정할 수 있음.</p>
<pre><code class="language-typescript">function sum(...numbers: number[]): number {
  return numbers.reduce((acc, num) =&gt; acc + num, 0);
}

console.log(sum(1, 2, 3));      // 6
console.log(sum(10, 20, 30));   // 60
</code></pre>
<p>위 코드에서 <code>sum</code> 함수는 가변 인자(<code>...number</code>)를 받아서 배열로 처리하며, 각 요소는 <code>number</code> 타입임. 여러 개의 숫자를 전달하면 그 합을 구하는 함수임.</p>
<p>&lt;&gt;function sum(num1, num2, ...numbers)</p>
<hr />
<h4 id="6️⃣-유니온-타입">6️⃣ 유니온 타입</h4>
<p>: 하나 이상의 타입을 허용함</p>
<h4 id="7️⃣-인터페이스를-통한-타입-지정">7️⃣ 인터페이스를 통한 타입 지정</h4>
<p>: 복잡한 객체 형태의 파라미터에 인터페이스 사용할 수 있음.</p>
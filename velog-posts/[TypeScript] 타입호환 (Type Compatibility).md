<h1 id="타입호환-type-compatibility">타입호환 (Type Compatibility)</h1>
<h3 id="타입간의-호환-여부-변수에-특정-값을-할당할-수-있는지의-관점">타입간의 호환 여부, 변수에 특정 값을 할당할 수 있는지의 관점</h3>
<pre><code class="language-typescript">let a: number = 10;
let b: string = 'hi';
b=a; //에러 발생. 호환되지 않음</code></pre>
<p><span style="color: red;">Q. 이 코드에서 에러가 발생하는데 그 이유는?</span>
  A.<del><span style="color: gray;"><code>a</code>는 <code>number</code> 타입으로 선언되어 숫자 값인 <code>10</code>을 가지고 있는데, <code>b</code>는 <code>string</code> 타입으로 선언되어 문자값인 <code>'hi'</code>를 가지고 있다. 
  즉,<strong><code>a</code>변수와 <code>b</code>변수의 타입이 다르기 때문에</strong> 발생하는 에러이다.</span></del></p>
<hr />
<h2 id="유니온union-타입">유니온(Union) 타입</h2>
<p>자바스크립트의 <code>OR 연산자(||)</code>와 같이 <code>'A'</code> 이거나 <code>'B'</code>이다 라는 의미의 <strong>하나 이상의 타입이 될 수 있는 값</strong>을 표현함.</p>
<p>타입호환성 관점에서보면, 유니온 타입은 가각가의 타입 중 하나라도 맞으면 호환될 수 있음.</p>
<pre><code class="language-typescript">function logText(text: string | number) {
  // ...
}</code></pre>
<p>  <span style="color: red;">Q. 유니온 타입을 사용해야 하는 이유는?</span>
  A. <del><span style="color: gray;">유니온 타입을 사용하면 하나의 변수나 함수가 <strong>여러 타입</strong>을 받을 수 있음.
  예를 들어, <code>number</code>와 <code>string</code> 타입을 모두 처리해야 할 때 유니온 타입이 유용함.</span></del></p>
<pre><code class="language-typescript">  function getAge(age: number | string) {
   if(typeof age == ‘number’) {
    return age.toFixed(); // 정상 동작, age의 타입이 ‘number’로 추론되기 때문에 number 관련된 API를 쉽게 자동완성 할 수 있음
   }

   if(typeof age == 'string') {
     return age; // 문자열 그대로 반환
   }

   return new TypeError('age must be number of string'); // 타입에러 코드</code></pre>
<p>이처럼 유니온 타입을 사용하면 타입스크립트의 장점을 살릴 수 있음.</p>
<hr />
<p>➕ <em><strong>타입에러 코드란?</strong></em>
JavaScript와 TypeScript에서 발생하는 오류 중 하나로, 값이나 연산이 올바른 데이터 타입이 아닐 때 발생하는 오류임.TypeScript에서는 주로 <code>타입 안정성을 보장</code>하기 위해 사용되기도 함.</p>
<p>주로 다음과 같은 경우에 사용됨</p>
<blockquote>
<ul>
<li>함수에 <strong>잘못된 타입의 인자가 전달</strong>되었을 때.</li>
</ul>
</blockquote>
<ul>
<li>객체에서 <strong>존재하지 않는 속성이나 메서드를 호출</strong>하려고 할 때.</li>
<li><code>null</code> 또는 <code>undefined</code>에 대해 프로퍼티에 접근하려고 할 때.</li>
</ul>
<pre><code class="language-typescript">  // number나 string이 아닌 타입이 들어온 경우
  return new TypeError('age must be number or string');
}</code></pre>
<p> <code>age</code>가 <code>number</code>또는 <code>string</code>일 때는 문제가 없지만, <code>boolean</code>, <code>object</code>, <code>undefined</code> 등의 타입이 잘못 들어왔을 때는 TypeError가 발생함.</p>
<p><span style="color: red;">Q. 타입에러 코드를 사용하였을때의 장점은?</span>
A. <span style="color: gray;"><del>함수가 올바른 타입의 값을 받지 못했을 경우에 경고할 수 있음.
명시적 오류 메시지를 통해 문제를 쉽게 추적하고 해결할 수 있게 도와줌.</del></span></p>
<hr />
<h2 id="인터섹션intersection-타입">인터섹션(intersection) 타입</h2>
<p>인터섹션 타입(Intersection Type)은 여러 타입을 모두 만족하는 하나의 타입을 의미함. 즉, 인터섹션 타입은 여러 타입의 <strong>모든 속성을 합친 타입</strong>임.</p>
<p>타입 호환성 관점에서 보면, 인터섹션 타입은 두 타입의 <strong>공통 부분을 만족해야만 호환</strong> 가능함.</p>
<pre><code class="language-typescript">  interface Person {
      name: string;
      age: number;
  }

  interface Developer {
      name: string;
      skill: number;
  }

  type Capt = Person &amp; Developer;</code></pre>
<p>  위의 예시 코드에서는 <code>Person</code> 인터페이스의 타입 정의와 <code>Developer</code> 인터페이스의 타입 정의를 <strong><code>&amp;</code> 연산자를 이용하여 합친 후 <code>Capt</code> 라는 타입에 할당</strong>하였음.</p>
<p>결과적으로 <code>Capt</code>의 타입은 아래와 같음.</p>
<pre><code class="language-typescript">{
  name: string;
  age: number;
  skill: string;
}</code></pre>
<p>이처럼 <code>&amp;</code> 연산자를 이용해 <strong>여러 개의 타입 정의를 하나로 합치는 방식</strong>을 인터섹션 타입을 정의할 수 있음.</p>
<hr />
<blockquote>
</blockquote>
<ul>
<li>유니온 타입은 <strong>여러 타입 중 하나</strong>를 허용하는 방식으로 <strong>타입 호환이 유연함</strong>.</li>
<li>인터섹션 타입은 <strong>여러 타입의 속성을 모두 가져야 하므로</strong> 더 엄격함.</li>
</ul>
<h2 id="타입별칭type-aliases이란">타입별칭(Type Aliases)이란?</h2>
<h4 id="특정-타입에-대해-새로운-이름을-붙여주는-기능">특정 타입에 대해 새로운 이름을 붙여주는 기능</h4>
<p>복잡한 타입을 더 간결하고 직관적인 이름으로 재사용할 수 있음. </p>
<pre><code class="language-typescript">type User = {
  name: string;
  age: number;
};

const user: User = {
  name: &quot;Alice&quot;,
  age: 30
};
</code></pre>
<p><code>type User</code>는 객체의 타입을 정의한 타입 별칭임. 이후 <code>User</code>를 타입으로 사용해 <code>user</code>라는 변수에 그 구조를 따르는 값을 할당함.</p>
<hr />
<h3 id="타입-확장">타입 확장(&amp;)</h3>
<p>기존 타입에 새로운 속성을 추가하거나 변형할 수 있음. 주로 <strong>인터섹션 타입</strong>을 사용해 타입을 확장함.</p>
<pre><code class="language-typescript">type Person = {
  name: string,
  age: number
}

type Student = Person &amp; { // 확장(상속)
  school: string
}

const jieun: Student = {
  name: 'jieun',
  age: 27,
  school: 'HY'
}</code></pre>
<h4 id="❗️❗️-그러나-type은-span-stylecolorgray인터페이스와-달리span-선언적-확장이-불가능함">❗️❗️ 그러나 <strong>type</strong>은 <span style="color: gray;"><del>인터페이스와 달리</del></span> 선언적 확장이 불가능함</h4>
<blockquote>
<p>타입 별칭은 그 자체로 완전한 정의이기 때문에 새로운 선언을 통해 확장하거나 병합할 수 없음.</p>
</blockquote>
<pre><code class="language-typescript">type User = {
  name: string;
};

// 새로운 속성을 추가하려고 시도해도 오류 발생
type User = {
  age: number;
}; // Error: Duplicate identifier 'User'.
</code></pre>
<p>이처럼 타입 별칭은 한 번 정의되면 같은 이름으로 다시 선언해 확장할 수 없음.</p>
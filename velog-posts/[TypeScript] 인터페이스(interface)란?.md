<h2 id="인터페이스interface란">인터페이스(interface)란?</h2>
<h4 id="객체-모양의-타입을-정의할-때-유용한-문법">객체 모양의 타입을 정의할 때 유용한 문법</h4>
<p>프레임워크(<span style="color: gray;">리액트, 뷰 ... 등등</span>)에서는 주로 <code>API 응답</code>, <code>프롭스</code>, <code>변수</code>, <code>함수</code>를 정의할 때 자주 사용함.</p>
<pre><code class="language-typescript">interface Person {
  name: string;
  age: number;
}

const vision: Person= {
  name: '비전',
  age: 3
};</code></pre>
<hr />
<h3 id="인터페이스-확장extends">인터페이스 확장(extends)</h3>
<p>js 클래스에서 상속을 할 때 *<em><code>extends</code> *</em>키워드를 사용하는데 인터페이스에서도 사용해주면 됨.</p>
<pre><code class="language-typescript">interface Person {
   name: string;
}

interface Developer extends Person {
   skill: string;
}

let fe: Developer = { name: 'josh', skill: 'TypeScript' };</code></pre>
<h4 id="➕--인터페이스-확장은-여러-개-_extends_가-가능함">➕  인터페이스 확장은 여러 개 _<code>extends</code>_가 가능함.</h4>
<p>(참고로 클래스는 반드시 하나만 extends 할 수 있음)</p>
<pre><code class="language-typescript">interface Person {
   name: string;
   age: number;
}

interface Programmer {
   favoriteProgrammingLanguage: string;
}

interface Korean extends Person, Programmer { // 두개의 인터페이스를 받아 확장
   isLiveInSeoul: boolean;
}

const person: Korean = {
   name: '홍길동',
   age: 33,
   favoriteProgrammingLanguage: 'kor',
   isLiveInSeoul: true,
};</code></pre>
<hr />
<h3 id="인터페이스-선언-병합-interface-declararion-merging">인터페이스 선언 병합 (interface Declararion Merging)</h3>
<p>동일한 이름을 가진 인터페이스를 여러 번 선언하면, TypeScript가 이를 <strong>자동으로 병합하여 하나의 인터페이스로 처리</strong>하는 기능</p>
<blockquote>
<p><strong>같은 이름을 가진 인터페이스</strong>를 <strong>여러 번 선언</strong>할 수 있으며, 
이 인터페이스들은 병합되어 하나의 확장된 형태로 동작.</p>
</blockquote>
<pre><code class="language-typescript">interface User {
  name: string;
}

interface User {
  age: number;
}

const user: User = {
  name: &quot;Alice&quot;,
  age: 30
};
</code></pre>
<p>위 코드에서 <code>User</code>라는 인터페이스를 두 번 선언했지만, TypeScript는 이를 <strong>병합</strong>하여 <code>name</code>과 <code>age</code> 속성을 모두 가지는 하나의 <code>User</code> 인터페이스로 처리함.</p>
<h2 id="객체타입-프롭스props란">객체타입 프롭스(props)란?</h2>
<h3 id="컴포넌트가-전달받는-데이터가-객체-형태일-때의-프롭스를-의미">컴포넌트가 전달받는 데이터가 객체 형태일 때의 프롭스를 의미</h3>
<p>Q.<span style="color: red;"> 객체 타입 프롭스를 사용하는 이유는? </span>
A. <del><span style="color: gray;">여러 속성을 한 번에 전달하고 그 속성들을 개별적으로 사용할 수 있다는 장점이 있음. 특히 복잡한 데이터를 처리할 때 <strong>객체</strong>를 사용하여 여러 값을 <code>하나의 프롭스</code>로 전달하는 방식이 유용함.</span></del></p>
<pre><code class="language-typescript">interface UserProps {
  name: string;
  age: number;
}

function UserInfo(props: UserProps) {
  return (
    &lt;div&gt;
      &lt;p&gt;Name: {props.name}&lt;/p&gt;
      &lt;p&gt;Age: {props.age}&lt;/p&gt;
    &lt;/div&gt;
  );
}</code></pre>
<ul>
<li><code>UserProps</code>는 <code>name</code>과 <code>age</code>라는 두 가지 속성을 포함하는 객체 타입의 프롭스.</li>
<li><code>UserInfo</code> 컴포넌트는<code>name</code>과 <code>age</code>객체를 전달받아 내부에서 <strong><code>props.name</code></strong>과<strong><code>props.age</code></strong> 로 해당 값을 사용할 수 있음.</li>
</ul>
<hr />
<h3 id="➕-구조-분해-할당-가능"><strong>➕ 구조 분해 할당 가능</strong></h3>
<pre><code class="language-typescript">function UserInfo({ name, age }: UserProps) {
  return (
    &lt;div&gt;
      &lt;p&gt;Name: {name}&lt;/p&gt;
      &lt;p&gt;Age: {age}&lt;/p&gt;
    &lt;/div&gt;
  );
}
</code></pre>
<ul>
<li>구조 분해 할당을 사용하면 <code>props</code> 객체에서 <code>name</code>과 <code>age</code>라는 속성을 바로 꺼내서 사용할 수 있음.
(원래는 <code>props.name</code>, <code>props.age</code>와 같이 사용)</li>
</ul>
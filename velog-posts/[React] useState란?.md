<h3 id="usestate란">useState란?</h3>
<p><code>useState</code>는 React의 상태(state) 관리 함수로, 컴포넌트의 상태를 저장하고 변경할 수 있도록 도와주는 <strong>React Hook</strong>임.</p>
<h3 id="📌-usestate-의-기본-사용법">📌 <code>useState</code> 의 기본 사용법</h3>
<pre><code class="language-javascript">import { useState } from &quot;react&quot;;

const Counter = () =&gt; {
  // count 상태를 선언하고, 초기값을 0으로 설정
  const [count, setCount] = useState(0);

  return (
    &lt;div&gt;
      &lt;p&gt;현재 카운트: {count}&lt;/p&gt;
      &lt;button onClick={() =&gt; setCount(count + 1)}&gt;+1 증가&lt;/button&gt;
    &lt;/div&gt;
  );
};

export default Counter;</code></pre>
<ol>
<li><code>useState(0)</code> 을 이용해서 <code>count</code> 상태 변수를 만들고, 초기값을 <code>0</code>으로 설정함</li>
<li><code>setCount</code> 함수를 이용해 <code>count</code> 값을 변경할 수 있음</li>
<li>버튼을 클릭하면 <code>setCount(count+1)</code> 이 실행되어 숫자가 1씩 증가함</li>
</ol>
<hr />
<h3 id="📌-usestate-상세-설명">📌 <code>useState</code> 상세 설명</h3>
<p>1️⃣ <strong><code>useState</code> 의 기본 형태</strong></p>
<pre><code class="language-javascript">const [state, setState] = useState(intialValue);</code></pre>
<ul>
<li><code>state</code>: 현재 상태 값을 저장하는 변수</li>
<li><code>setState</code>: 상태를 변경하는 함수</li>
<li><code>initialValue</code>: 상태의 초기값</li>
</ul>
<p><strong>예제 살펴보기</strong></p>
<ol>
<li>문자열 상태</li>
</ol>
<pre><code class="language-javascript">const  [name, setName] = useState(&quot;Wonbin&quot;);

setName(&quot;Park&quot;); // 상태 변경 -&gt; 화면 다시 렌더링 됨</code></pre>
<ol start="2">
<li>boolean 값 상태(true/false)<pre><code class="language-javascript">const [isVisible, setIsVisible] = useState(false);
</code></pre>
</li>
</ol>
<p>setIsVisible(true); // 상태 변경</p>
<pre><code>
**2️⃣ `useState` 에서 객체 사용하기**
```javascript
const [user, setUser] = useState({ name: &quot;Wonbin&quot;, age: 24});

const updateAge = () =&gt; {
    setUser({...user, age:user.age + 1}); // 기존 객체 복사 후 age만 변경
}</code></pre><blockquote>
<h3 id="span-stylecolorred주의할-점span"><strong><span style="color: red;">주의할 점</span></strong></h3>
<p><code>setUser(user.age = 23);</code> 과 같은 형식으로는 해선 안됨!
React는 상태가 직접 변경되면 <strong>변경을 감지하지 못하므로</strong> 반드시 <code>setState</code>를 사용해주어야 함!</p>
</blockquote>
<p><strong>3️⃣ <code>useState</code>에서 배열 사용하기</strong></p>
<pre><code class="language-javascript">const [items, setItems] = useState([&quot;사과&quot;, &quot;바나나&quot;]);

const addItem = () =&gt; {
    setItems([...items, &quot;포도&quot;]); // 기존 배열을 복사힌 후 새로운 값 추가
}</code></pre>
<p>=&gt; 배열을 업데이트할 때는 <strong>기존 배열을 복사하고 새 값을 추가</strong>해야 함.
(React는 기존 상태와 새로운 상태를 비교하여 변경된 부분만 렌더링하기 때문임)</p>
<hr />
<h3 id="usestate에서-상태-변경하는-방법"><code>useState</code>에서 상태 변경하는 방법</h3>
<h4 id="기본적인-상태-변경">기본적인 상태 변경</h4>
<pre><code class="language-javascript">setCount(5); // count 값을 5로 변경</code></pre>
<h4 id="이전-상태를-기반으로-변경-함수형-업데이트">이전 상태를 기반으로 변경 (함수형 업데이트)</h4>
<pre><code class="language-javascript">setCount(prevCount =&gt; prevCount + 1);</code></pre>
<ul>
<li>이렇게 하면 최신 상태 값을 기반으로 안전하게 업데이트 할 수 있음.</li>
<li>여러 번 setCount(count+1)을 호출하면 한 번만 업데이트 될 수 있으므로, <strong>함수형 업데이트</strong>를 사용하면 좋음!</li>
</ul>
<pre><code class="language-javascript">setCount(prev =&gt; prev + 1);
setCount(prev =&gt; prev + 1);
setCount(prev =&gt; prev + 1);</code></pre>
<p>=&gt; 이렇게 하면 <code>count</code>값이 3씩 증가하게 됨</p>
<hr />
<h3 id="usestate-사용-시-주의할-점"><code>useState</code> 사용 시 주의할 점</h3>
<ol>
<li>상태를 직접 변경해서는 안됨!<pre><code class="language-javascript">const [user, setUser] = useState({ name: &quot;Wonbin&quot;, age: 24 });
</code></pre>
</li>
</ol>
<p>user.age = 24; // 다음과 같은 방식 ❌</p>
<pre><code>=&gt; 이렇게 하면 React가 변경을 하지 못해서 화면이 업데이트 되지 않음.
✅ 올바른 방법:
```javascript
setUser({...user, age: 23 });</code></pre><ol start="2">
<li>상태 변경은 비동기적으로 처리됨<pre><code class="language-javascript">console.log(count);
setCount(count + 1);
console.log(count); // 여전히 이전 값이 출력됨</code></pre>
=&gt; 상태가 바로 업데이트 되는 것이 아니라 <strong>비동기</strong>적으로 처리되므로 <code>setCount</code> 후 바로 <code>console.log(count)</code>를 하면 이전 값이 출력될 수 있음.</li>
</ol>
<p>✅ 올바른 방법:</p>
<pre><code class="language-javascript">useEffect(() =&gt; {
  console.log(&quot;count 값이 변경됨:&quot;, count);
}, [count]); // count 값이 변경될 때 실행됨</code></pre>
<p>=&gt; 상태 변경 후 실행되는 효과를 보고 싶다면 <code>useEffect</code> 사용</p>
<hr />
<h3 id="usestate-실전-예제"><code>useState</code> 실전 예제</h3>
<p><strong>1️⃣ 입력값을 관리하는 상태</strong></p>
<pre><code class="language-javascript">const InputBox = () =&gt; {
  const [text, setText] = useState(&quot;&quot;);

  return (
    &lt;div&gt;
      &lt;input
        type=&quot;text&quot;
        value={text}
        onChange={(e) =&gt; setText(e.target.value)}
      /&gt;
      &lt;p&gt;입력한 값: {text}&lt;/p&gt;
    &lt;/div&gt;
  );
};</code></pre>
<p>=&gt; 사용자가 입력한 값을 <code>text</code> 상태에 저장하고 화면에 반영</p>
<p><strong>2️⃣ 배열에서 데이터 추가하기</strong></p>
<pre><code class="language-javascript">import { useState } from &quot;react&quot;;

const TodoList = () =&gt; {
  const [todos, setTodos] = useState([&quot;공부하기&quot;, &quot;운동하기&quot;]);

  const addTodo = () =&gt; {
    setTodos([...todos, &quot;새로운 할 일&quot;]); // 기존 배열 복사 후 새로운 값 추가
  };

  return (
    &lt;div&gt;
      &lt;ul&gt;
        {todos.map((todo, index) =&gt; (
          &lt;li key={index}&gt;{todo}&lt;/li&gt;
        ))}
      &lt;/ul&gt;
      &lt;button onClick={addTodo}&gt;할 일 추가&lt;/button&gt;
    &lt;/div&gt;
  );
};</code></pre>
<p>=&gt; <code>setTodos([...todos, &quot;새로운 할 일&quot;])</code>을 사용하여 기존 배열을 유지하면서 새로운 항목을 추가</p>
<hr />
<blockquote>
<p>‼️ <strong>useState</strong> 정리</p>
</blockquote>
<ul>
<li><code>useState</code> : React의 상태 관리 Hook</li>
<li>사용 방법: <code>const [state, setState] = useState(초기값)</code></li>
<li>상태 변경: <code>setState(새로운 값)</code></li>
<li>이전 값 기반 업데이트: <code>setState(prev =&gt; prev + 1)</code> </li>
<li>객체 업데이트: <code>setState({...state, 변경할 값})</code></li>
<li>배열 업데이트: <code>setState([...state, 새로운 값])</code></li>
</ul>
<p>✔️ <code>useState</code>는 React에서 가장 기본적이면서 중요한 Hook!
✔️ 상태를 직접 변경하지 말고 항상 <code>setState</code>를 사용해야 함
✔️ 상태 변경은 <strong>비동기적으로 처리됨</strong>을 항상 기억!</p>
<h2 id="🔥useeffect-완전-정복🔥">🔥<code>useEffect</code> 완전 정복!🔥</h2>
<p>React에서 <code>useEffect</code>는 <strong>컴포넌트의 생명주기</strong>를 다룰 때 사용하는 Hook임
예를 들어, <strong>컴포넌트가 렌더링 될 때 데이터 가져오기</strong>, <strong>DOM 업데이트</strong> 같은 부수효과(side effect)를 실행할 때 사용됨</p>
<h3 id="useeffect는-언제-쓰나요"><code>useEffect</code>는 언제 쓰나요?</h3>
<p>1️⃣ <strong>컴포넌트가 처음 렌더링</strong>될 때 실행 (<code>ex</code>API에서 데이터 가져오기)
2️⃣ <strong>특정 값이 변경</strong>될 때 실행 (<code>ex</code> state나 props가 변경될 때 반응)
3️⃣ <strong>컴포넌트가 사라질 때</strong> 정리(clean-up) 작업 수행 (<code>ex</code> 이벤트 리스너 제거, 타이머 제거)</p>
<h4 id="useeffect-기본-문법"><code>useEffect</code> 기본 문법</h4>
<pre><code class="language-javascript">import { useEffect } from &quot;react&quot;;

useEffect(() =&gt; {
  // 여기에 실행할 코드 작성
});</code></pre>
<p>✔️ 이렇게만 작성하면?
=&gt; 렌더링될 때마다 실행됨 (원하지 않는 불필요한 실행이 생길 수도 있음!)</p>
<h4 id="useeffect-실행-시점-컨트롤하기"><code>useEffect</code> 실행 시점 컨트롤하기</h4>
<p>1️⃣ 마운트(처음 렌더링) 시 한 번만 실행</p>
<pre><code class="language-javascript">useEffect(() =&gt; {
  console.log(&quot;컴포넌트가 처음 렌더링됨!&quot;);
}, []);</code></pre>
<p>✔️ <code>[]</code>(의존성 배열)이 비어 있으면 <strong>한 번만 실행됨</strong>
✔️ 컴포넌트가 <strong>처음 나타날 때만 실행</strong>하고, <strong>이 후에는 실행되지 않음</strong></p>
<p>2️⃣ 특정 값이 변경될 때 실행</p>
<pre><code class="language-javascript">useEffect(()=&gt;{
    console.log(`count 값이 변경됨:', ${count}`);
}, [count]);</code></pre>
<p>✔️ <code>count</code> 값이 변경될 때마다 <code>useEffect</code>가 실행됨
✔️ <code>count</code> 가 변경되지 않으면 실행되지 않음</p>
<p>3️⃣ 언마운트 시(컴포넌트가 사라질 때) 정리(clean-up)</p>
<pre><code class="language-javascript">import { useEffect } from &quot;react&quot;;

useEffect(() =&gt; {
  const interval = setInterval(() =&gt; {
    console.log(&quot;1초마다 실행 중...&quot;);
  }, 1000);

  return () =&gt; {
    clearInterval(interval);
    console.log(&quot;타이머가 제거됨!&quot;);
  };
}, []);</code></pre>
<p>✔️ <code>return</code> 안에 있는 함수는 <strong>컴포넌트가 사라질 때 실행됨</strong>
✔️ 주로 이벤트 리스너 제거, 타이머 정리, 웹소켓 연결 종료 등에 사용됨</p>
<hr />
<h4 id="실전-예제">실전 예제!</h4>
<p>1️⃣ API 데이터 가져오기 (처음 렌더링 시 한 번만 실행)</p>
<pre><code class="language-javascript">import { useEffect, useState } from &quot;react&quot;;

const App = () =&gt; {
  const [data, setData] = useState(null);

  useEffect(() =&gt; {
    fetch(&quot;https://jsonplaceholder.typicode.com/todos/1&quot;)
      .then((response) =&gt; response.json())
      .then((json) =&gt; setData(json));
  }, []);

  return &lt;div&gt;{data ? JSON.stringify(data) : &quot;로딩 중...&quot;}&lt;/div&gt;;
};</code></pre>
<p>2️⃣ 윈도우 크기 변경 감지 (특정 값 변경 시 실행)</p>
<pre><code class="language-javascript">import { useEffect, useState } from &quot;react&quot;;

const App = () =&gt; {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() =&gt; {
    const handleResize = () =&gt; setWidth(window.innerWidth);

    window.addEventListener(&quot;resize&quot;, handleResize);

    return () =&gt; {
      window.removeEventListener(&quot;resize&quot;, handleResize);
    };
  }, []);

  return &lt;div&gt;현재 창 너비: {width}px&lt;/div&gt;;
};</code></pre>
<p>✔️ <code>window.addEventListener</code> 추가
✔️ 컴포넌트가 사라질 때 <code>removeEventListener</code>로 정리(clean-up)</p>
<hr />
<blockquote>
<p>✅ 정리</p>
</blockquote>
<ul>
<li><code>useEffect(() =&gt; {...})</code> : 매 렌더링마다 실행</li>
<li><code>useEffect(() =&gt; {...}, [])</code> : 처음 한 번만 실행 (마운트 시)</li>
<li><code>useEffect(() =&gt; {...}, [변수])</code> : 특정 겂아 변경될 때 실행</li>
<li><code>useEffect(() =&gt; { return () =&gt; {...}}, [])</code> : 언마운트 시 정리 작업 수행</li>
</ul>
<p>‼️<code>useEffect</code> 사용 시 주의할 점</p>
<ol>
<li>의존성 배열을 정확하게 설정해야 함</li>
</ol>
<ul>
<li>의존성 배열을 실수로 빠뜨리면 원치 않는 반복 실행이 발생할 수 있음</li>
</ul>
<ol start="2">
<li>클린업 함수(return)를 잘 활용해야 함</li>
</ol>
<ul>
<li>이벤트 리스너, 타이머 등을 정리하지 않으면 메모리 누수 발생 가능</li>
</ul>
<ol start="3">
<li>불필요한 렌더링을 방지해야 함</li>
</ol>
<ul>
<li><code>useEffect</code> 내에서 상태(state)를 변경하면 무한 루프가 발생할 수 있음</li>
</ul>
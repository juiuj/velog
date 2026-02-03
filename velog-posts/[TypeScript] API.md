<h2 id="api란">API란?</h2>
<p><code>API(Application Programming Interface)</code> 란, 쉽게 말해서 <strong>컴퓨터들이 서로 대화할 수 있도록 도와주는 방법</strong> 이라고 볼 수 있음.</p>
<p>예를 들어,
<img alt="" src="https://velog.velcdn.com/images/dev-joohee/post/ab2d89ab-1d00-4f80-9899-8475f949e0a6/image.png" />
피자 가게에서 피자를 주문할 때, 우리는 메뉴판을 보고 원하는 피자를 선택하고, 그 피자의 이름과 사이즈 등을 직원에게 말함. 그러면 직원은 우리가 말한 주문대로 피자를 만들어 줌. 여기서 API는 우리와 피자 가게 사이에서 서로 대화를 돕는 <code>메뉴판과 직원</code> 같은 역할을 함.</p>
<ul>
<li><strong>피자가게</strong>: 우리가 주문하고 싶은 정보나 서비스를 제공하는 곳 <span style="color: skyblue;">(<code>ex</code> 인터넷의 어떤 서비스나 웹)</span></li>
<li><strong>주문서</strong>: 우리가 피자를 어떻게 만들지 알려주는 정보 <span style="color: skyblue;">(API를 통해 우리가 요청하는 것)</span></li>
<li><strong>피자 완성</strong>: 주문서대로 만든 피자를 우리에게 전달하는 것 <span style="color: skyblue;">(API가 우리에게 결과를 보내주는 것)</span></li>
</ul>
<hr />
<h3 id="rest-api란">REST API란?</h3>
<p>REST(Representational State Transfer) API는 클라이언트와 서버 간에 데이터를 주고 받기 위한 URL 규칙임.
하이퍼 미디어(링크)를 기반으로 특정 리소스나 데이터를 접근하기 위한 방식으로써 <code>URL</code>에 명시적으로 어떤 데이터를 담고 있는지 나타내야 함.</p>
<p>예를 들어, 사용자의 목록을 받아오는 URL은 다음과 같음</p>
<pre><code>http://domain.com/api/users
</code></pre><p>여기서 첫 번째 사용자 데이터는 다음과 같이 접근할 수 있음.</p>
<pre><code class="language-code">http://domain.com/api/users/1
</code></pre>
<hr />
<h3 id="api-함수-예시">API 함수 예시</h3>
<p><a href="https://jsonplaceholder.typicode.com/todos">https://jsonplaceholder.typicode.com/todos</a>
<img alt="" src="https://velog.velcdn.com/images/dev-joohee/post/0746d8df-6b81-4d4f-8e99-0311455fa4d0/image.png" /></p>
<pre><code class="language-typescript">const apiUrl: string = 'https://jsonplaceholder.typicode.com/todos';

interface Todo { // API에서 반환하는 Todo 객체의 구조 정의. 해당 인터페이스는 각 할 일 항목이 다음 속성들을 가지고 있음을 명시함.
  userId: number;
  id: number;
  title: string;
  completed: boolean;
}  

//TODO: 아래 API 함수의 타입을 정의해 보세요
async function fetchTodos(): Promise&lt;Todo[]&gt; { 
  const response = await fetch(apiUrl);
  const data = await response.json();
  return data;
}  

fetchTodo().then(todos =&gt; todos[0].id);
</code></pre>
<p>이 코드에서는 </p>
<ul>
<li><p><code>async</code> 키워드를 사용하여 함수가 비동기로 동작함을 나타내며, <code>await</code>로 비동기 작업을 처리함.</p>
</li>
<li><p><code>fetch(apiUrl)</code>을 사용하여 <code>apiUrl</code>에 GET 요청을 보내고, 응답을 받아서 <code>response</code> 변수에 저장함.</p>
</li>
<li><p><code>response.json()</code>은 응답 데이터를 JSON 형식으로 변환하여, 그 결과를 <code>data</code> 변수에 저장함.</p>
</li>
<li><p>함수는 <code>Promise&lt;Todo[]&gt;</code> 타입을 반환함. 즉, 이 함수는 할 일 목록(Todo)의 배열을 포함하는 프로미스를 반환하고, 반환되는 데이터는 <code>Todo</code> 인터페이스와 일치하는 구조로 되어 있음.</p>
</li>
<li><p><code>fetchTodos().then()</code> 함수가 비동기적으로 데이터를 가져오면 <code>.then()</code> 블록에서 할 일 목록을 처리할 수 있음.
<span style="color: gray;"> 여기서는 첫 번째 할 일 항목의 <code>id</code> 값을 가져옴.</p>
</li>
</ul>
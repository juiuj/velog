<h2 id="📡-웹소켓websocket이란">📡 웹소켓(WebSocket)이란?</h2>
<p>웹소켓은 웹에서 클라이언트(브라우저)와 서버가 실시간으로 양방향 통신을 할 수 있게 해주는 프로토콜</p>
<p>일반 HTTP 통신과 다르게 한 번 연결되면 끊어지지 않고 계속 연결을 유지하면서 서로 자유롭게 데이터를 주고 받을 수 있다는 것이 가장 큰 특징.</p>
<h3 id="✅-왜-필요한가">✅ 왜 필요한가?</h3>
<ul>
<li>실시간 채팅</li>
<li>실시간 알림</li>
<li>주식 시세, 실시간 데이터 스트리밍</li>
<li>위치 추적 서비스</li>
</ul>
<h3 id="🔥-typescript에서-웹소켓-연결하는-기본-구조">🔥 TypeScript에서 웹소켓 연결하는 기본 구조</h3>
<pre><code class="language-typeScript">// 웹소켓 인스턴스 생성
const socket = new WebSocket('ws://서버주소:포트');

// 연결 성공 시
socket.addEventListener('open', (event: Event) =&gt; {
  console.log('웹소켓 연결 성공');
  socket.send('클라이언트에서 보낸 메시지');
});

// 메시지 수신 시
socket.addEventListener('message', (event: MessageEvent) =&gt; {
  console.log('서버로부터 받은 메시지:', event.data);
});

// 에러 발생 시
socket.addEventListener('error', (event: Event) =&gt; {
  console.error('웹소켓 에러:', event);
});

// 연결 종료 시
socket.addEventListener('close', (event: CloseEvent) =&gt; {
  console.log('웹소켓 연결 종료:', event.code, event.reason);
});
</code></pre>
<h3 id="✅-웹소켓-상태-확인">✅ 웹소켓 상태 확인</h3>
<pre><code class="language-typeScript">if (socket.readyState === WebSocket.OPEN) {
  socket.send('이미 연결되어 있음');
}
</code></pre>
<h3 id="✅-사용자-정의-타입으로-메시지-다루기">✅ 사용자 정의 타입으로 메시지 다루기</h3>
<pre><code class="language-typeScript">// 예: 서버로부터 오는 JSON 데이터를 파싱할 경우
socket.addEventListener('message', (event: MessageEvent) =&gt; {
  const data: { type: string; payload: any } = JSON.parse(event.data);

  switch (data.type) {
    case 'chat':
      console.log('채팅 메시지:', data.payload);
      break;
    case 'notification':
      console.log('알림:', data.payload);
      break;
    default:
      console.warn('알 수 없는 메시지 유형');
  }
});</code></pre>
<h4 id="🙋-정리">🙋 정리</h4>
<ul>
<li><code>open</code> : 연결 성공 시</li>
<li><code>message</code> : 서버로부터 메시지 수신 시</li>
<li><code>error</code> : 에러 발생 시</li>
<li><code>close</code> : 연결 종료 시</li>
</ul>
<hr />
<h3 id="✅-react--typescript에서-웹소켓-사용하는-경우">✅ React + TypeScript에서 웹소켓 사용하는 경우</h3>
<h4 id="1️⃣-웹소켓을-어디서-생성할까">1️⃣ 웹소켓을 어디서 생성할까?</h4>
<p>보통 <code>useEffect</code> 훅 안에서 생성하고, 컴포넌트가 언마운트될 때 닫아주는 패턴 사용</p>
<pre><code class="language-Typescript">import React, { useEffect, useRef } from 'react';

const ChatComponent: React.FC = () =&gt; {
  const socketRef = useRef&lt;WebSocket | null&gt;(null);

  useEffect(() =&gt; {
    // 웹소켓 연결
    socketRef.current = new WebSocket('ws://서버주소:포트');

    socketRef.current.onopen = (event: Event) =&gt; {
      console.log('웹소켓 연결됨');
      socketRef.current?.send('안녕 서버야!');
    };

    socketRef.current.onmessage = (event: MessageEvent) =&gt; {
      console.log('받은 메시지:', event.data);
    };

    socketRef.current.onerror = (event: Event) =&gt; {
      console.error('에러 발생:', event);
    };

    socketRef.current.onclose = (event: CloseEvent) =&gt; {
      console.log('연결 종료:', event.code, event.reason);
    };

    // 클린업
    return () =&gt; {
      socketRef.current?.close();
    };
  }, []);

  return &lt;div&gt;채팅 중입니다...&lt;/div&gt;;
};
</code></pre>
<h3 id="2️⃣-메시지-데이터-타입-처리">2️⃣ 메시지 데이터 타입 처리</h3>
<p>서버가 JSON으로 데이터를 보낼 경우, <strong>타입</strong>을 명시해서 파싱하면 좋음</p>
<pre><code class="language-Typescript">type ServerMessage = {
  type: 'chat' | 'notification';
  payload: any;
};

socketRef.current.onmessage = (event: MessageEvent) =&gt; {
  const data: ServerMessage = JSON.parse(event.data);
  if (data.type === 'chat') {
    console.log('채팅 메시지:', data.payload);
  }
};
</code></pre>
<h3 id="➕-tip">➕ Tip</h3>
<ul>
<li><code>useRef</code>로 socket 인스턴스를 관리하면 다시 렌더링될 때도 인스턴스를 유지할 수 있음.</li>
</ul>
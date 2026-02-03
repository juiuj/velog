<p>웹 개발을 하다보면 URL 앞에 항상 붙는 <code>http://</code>, <code>https://</code>를 보게 된다.
겉보기에는 단순히<code>s</code> 하나 차이지만, 어떤 차이점이 있길래 <code>https</code>를 주로 쓰는걸까?</p>
<h1 id="http란-무엇인가">HTTP란 무엇인가?</h1>
<p><strong>HTTP(HyperText Transfer Protocol)</strong>는 클라이언트(브라우저)와 서버가 데이터를 주고 받기 위한 규칙(프로토콜)이다.</p>
<p>HTTP는 데이터를 <strong>✌️암호화하지 않고✌️</strong> 평문 그대로 전송하기 때문에 네트워크 중간에서 데이터가 그대로 노출될 수 있다. 그 때문에 <code>로그인 정보</code>, <code>개인정보</code>가 탈취될 위험이 존재한다.</p>
<blockquote>
<p>공용 와이파이 환경에서 HTTP 사이트에 로그인하면 아이디와 비밀번호가 <strong>그대로 노출</strong>💦 될 수 있음</p>
</blockquote>
<p>그래서 HTTP는 <strong>보안에 취약</strong>하다.</p>
<hr />
<h1 id="https란-무엇인가">HTTPS란 무엇인가?</h1>
<p>HTTPS의 <code>s</code>는 <code>secure</code>로, HTTP에 *<em>보안 계층(SSL/TLS) *</em>을 추가한 프로토콜이다.</p>
<p>HTTPS는 데이터가 <code>암호화되어 전송</code>되고, 그로 인해 중간에서 가로채도 내용을 해독할 수 없다는 특징이 있다. 또한 SSL/TLS 인증서와 CA를 통해 서버의 신뢰성 검증이 가능하다는 장점이 있다.
<del>닉값하는 프로토콜</del></p>
<h3 id="ssltls-인증서란">SSL/TLS 인증서란?</h3>
<p>SSL/TLS 인증서는 쉽게 말해 &quot;이 서버는 신뢰할 수 있는 서버&quot; 라는 것을 증명하는 전자 신분증 같은 거라고 볼 수 있다.</p>
<blockquote>
<p><strong>🔐 SSL</strong></p>
</blockquote>
<ul>
<li>SSL (Secure Sockets Layer)
  → 보안 소켓 계층</li>
<li>클라이언트와 서버 사이의 통신을 암호화하기 위해 만들어진 보안 프로토콜</li>
<li>HTTPS의 초기 보안 기술</li>
<li>현재는 보안 취약점 때문에 더 이상 사용되지 않음</li>
</ul>
<blockquote>
<p><strong>🔐 TLS</strong></p>
</blockquote>
<ul>
<li>TLS (Transport Layer Security)
  → 전송 계층 보안</li>
<li>SSL을 개선한 최신 보안 프로토콜</li>
<li>현재 HTTPS에서 실제로 사용되는 표준</li>
<li>더 강력한 암호화 방식과 보안 구조 제공</li>
</ul>
<p>HTTPS 통신에서 이 인증서를 통해 서버의 <code>신원 인증</code>, <code>데이터의 암호화</code>, <code>데이터의 무결설 보장</code> 이 세 가지가 가능해진다.</p>
<h3 id="인증서는-왜-필요한가">인증서는 왜 필요한가?</h3>
<p>만약 인증서가 없다면 어떻게 될까?
-&gt; 사용자는 접속한 서버가 진짜인지 알 수 없다. </p>
<p>예를 들어, 브라우저에서 <code>https://www.naver.com</code>에 접속하면, 네이버 서버는 <strong>SSL/TLS 인증서</strong>를 브라우저에 보내준다.</p>
<p>이 인증서에는 <strong>“이 서버는 <a href="http://www.naver.com%EC%9D%98">www.naver.com의</a> 서버다”</strong>라는 정보와 이를 <code>신뢰할 수 있는 인증기관(CA)</code>이 확인했다는 서명이 들어 있다.</p>
<p>브라우저는 이 인증서를 검증한 뒤에야 통신을 시작한다. 그래서 사용자는 <strong>진짜 네이버 서버와 통신 중이라는 것을 보장</strong>받을 수 있다❕</p>
<h3 id="ca-certificate-authority란">CA (Certificate Authority)란?</h3>
<p>인증서를 발급하고 관리하는 <strong>신뢰 기관</strong>으로, </p>
<ul>
<li>서버가 해당 도메인의 실제 소유자인지 확인</li>
<li>확인이 끝나면 인증서를 발급</li>
<li>인증서에 전자 서명 추가
👆 같은 역할을 한다. </li>
</ul>
<p>그래서 CA가 서명한 인증서라면 브라우저는 자동으로 서버를 신뢰하게 된다!</p>
<h2 id="https는-어떻게-동작할까">HTTPS는 어떻게 동작할까?</h2>
<p>앞서 말했다시피 HTTPS는 SSL/TLS라는 보안 프로토콜을 사용하는데, 
<code>SSL</code>란 초기 암호화 프로토콜로 설명할 수 있다. 현재는 거의 사용하지 않는 프로토콜이다.
<code>TLS</code>는 SSL을 개선한 <strong>⌜최신 표준 보안 프로토콜⌟</strong>로, 실제로 우리가 쓰는 HTTPS는 TLS기반이다!</p>
<blockquote>
<p>브라우저가 서버에 접속 -&gt; 서버가 SSL/TLS 인증서 전달 -&gt; 브라우저가 인증서 신뢰 여부 확인 -&gt; 암호화된 통신 시작 🔐</p>
</blockquote>
<hr />
<h2 id="http-vs-https-한눈에-비교">HTTP vs HTTPS 한눈에 비교</h2>
<p><del>지피티가 말아주는</del>
<img alt="" src="https://velog.velcdn.com/images/dev-joohee/post/fe9141a6-2200-4659-98ee-5d4bdcfefe61/image.png" /></p>
<hr />
<p>결론적으로, HTTP보다는 보안 + 사용자 신뢰 + 브라우저 정책까지 모두 고려하는 HTTPS를 사용하는 것이 좋다! </p>
<p>마무리.ㅋ
<img alt="" src="https://velog.velcdn.com/images/dev-joohee/post/0634600b-d2f8-4da3-ba92-236566b5a97a/image.png" /></p>
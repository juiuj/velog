<p>최근 <a href="https://wayout.kr/">WAyout 프로젝트</a>를 진행하며 개발이란 파면 팔 수록.. 공부할 게 정말 많다는 생각이 끝없이 든다. 프론트엔드로서 프로젝트를 진행하며 가장 취약하다고 느낀 부분은 바로 <strong>웹보안, 웹인증</strong> 관련 부분인데, 팀원들이 관련해서 질문을 할 때마다 식은땀이 줄줄 흐른다...;;;ㅜㅜ😅</p>
<p>오늘 공부해 볼 부분은 <strong>⌜왜 HttpOnly / SameSite / Secure 같은 옵션이 필요한가?⌟</strong> 이다.</p>
<p>이 공부를 통해서 쿠키 옵션 3개가 각각 어떤 공격을 막는지 한 번에 이해하고, 우리 서비스에서 쿠키를 쓴다면 어떤 조합으로 설정해야 하는 지 판단을 명확하게 할 수 있었으면 좋겠다<em>!</em></p>
<hr />
<h2 id="왜-쿠키-옵션-이야기를-해야-할까">왜 쿠키 옵션 이야기를 해야 할까?</h2>
<p>요즘 인증 구조를 보면 <code>OAuth 로그인</code>, 서버에서 <code>AccessToken</code>, <code>RefreshToken</code> 발급 -&gt; 토큰을 쿠키에 저장 -&gt; 브라우저는 요청마다 쿠키를 자동으로 전송...</p>
<p>문제는 여기서 끝이 아니다.</p>
<p>쿠키는 기본적으로 <strong>브라우저에 저장</strong>되고, 요청 시 자동으로 전송되며 설정을 잘못하면 <strong>보안 공격의 타깃</strong>이 될 수도 있다;;</p>
<p>그래서 등장한 게 바로
<code>HttpOnly</code>, <code>SameSite</code>, <code>Secure</code> 옵션이다.</p>
<p>쉽게 말해서 이 옵션들은 &quot;쿠키를 쓸 순 있는데, 아무렇게 쓰지는 말자~&quot;를 구현한 안전 장치 같은 거라고 볼 수 있다.</p>
<hr />
<h1 id="httponly란---js는-쿠키-건드리지말거라">HttpOnly란? - &quot;JS는 쿠키 건드리지말거라&quot;</h1>
<p><code>HttpOnly</code>는 말 그대로 <strong>JavaScript에서 쿠키에 접근하지 못하게 하는 옵션</strong> 이다.</p>
<h2 id="httponly-옵션이-왜-필요할까">HTTPOnly 옵션이 왜 필요할까?</h2>
<p><strong>&lt;XSS에서 토큰이 털리는 과정..&gt;</strong>
토큰이 JS에서 읽히는 위치에 있으면 *<code>XSS</code> 발생 시 토큰이 복제되어 탈취될 가능성이 매우 높다..!
즉, 토큰이 쿠키에 있어도 JS에서 읽을 수 있으면 XSS가 한방에 끝이다ㅜㅜ😭</p>
<p>*XSS: 공격자가 웹사이트에 악성 JavaScript를 주입해, 해당 사이트 사용자 권한으로 스크립트를 실행하게 만드는 취약점</p>
<p>그래서 인증 토큰을 쿠키에 넣는다면 <strong>HttpOnly는 거의 필수</strong>라고 볼 수 있다!</p>
<blockquote>
<p><code>HttpOnly</code>는 <strong>JS 접근 차단</strong>하고, XSS로부터 <strong>토큰 직접 탈취를 방어</strong>한다.
프론트에서 토큰을 읽을 수 없게 만드는 대신, 인증 판단은 서버나 응답 결과 기반으로 처리해야 한다!</p>
</blockquote>
<hr />
<h1 id="secure란---https에서만-보내라">Secure란? - &quot;HTTPS&quot;에서만 보내라</h1>
<p><code>Secure</code>옵션이 있으면 쿠키는 HTTP 요청에서는 포함되지 않고, <strong>HTTPS</strong> 요청에서만 전송된다.</p>
<h2 id="secure-옵션이-왜-필요할까">Secure 옵션이 왜 필요할까?</h2>
<p>이를 이해하기 위해선 HTTP와 HTTPS의 특징을 파악해야 한다.
지난 <a href="https://velog.io/@dev-joohee/HTTP%EC%99%80-HTTPS%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%84-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90">HTTPS 공부</a>를 참고하자~~</p>
<p>간단하게 살펴보자면,
HTTP는 암호화가 없어서 네트워크 구간에서 <strong>트래픽이 노출</strong>될 수 있다. 이때 쿠키가 평문으로 오가면 중간자 공격/스니핑 같은 방식으로 <strong>쿠키가 그대로 탈취될 위험</strong>이 있다.
그래서 전송 중 데이터 암호화가 가능한 <code>HTTPS</code>를 사용하게 되는데, <code>Secure</code>은 그 <strong>암호화 된 통신에서만 쿠키를 쓰겠다</strong> 라는 선언과 같은 것이다.</p>
<p>🙋‍♀️ 그래서 운영 환경에서는 사실상 <strong>쿠키 인증이면 Secure는 기본</strong>이라고 생각해도 좋을 것 같다.</p>
<hr />
<h1 id="samesite란---어디서-온-요청인지-살펴보자">SameSite란? - &quot;어디서 온 요청인지 살펴보자&quot;</h1>
<p><code>SameSite</code>는 이 쿠키가 어떤 도메인에서만 사용할 수 있는지 설정할 수 있는 옵션으로, <code>CSRF</code> 공격 방어와 관련되어 있다.</p>
<h3 id="왜-필요할까-csrf">왜 필요할까? (CSRF)</h3>
<blockquote>
<p>쿠키는 &quot;출처를 가리지 않고&quot; 자동 전송된다.</p>
</blockquote>
<p>즉, 사용자가 로그인된 상태일때 다른 사이트에서 요청이 발생할 경우, 조건만 맞으면 <strong>브라우저에서 쿠키가 같이 전송</strong>될 수 있다.</p>
<h2 id="samesite-옵션-3종류-👀">SameSite 옵션 3종류 👀</h2>
<p><strong>1️⃣ SameSite = Strict</strong>
다른 사이트에서 온 요청은 수락하지 않고, <strong>같은 사이트에서만 전송</strong>하는 옵션이다. (반드시 같은 도메인에서만 사용 가능)
Strict를 보면 알 수 있듯이 가장 강력해서 외부 링크, OAuth 리다이렉트에도 쿠키가 안 붙는다.
인증 흐름에서는 불편할 수 있지만, 보안은 최고❗️ <del>UX는 최악</del></p>
<p><strong>2️⃣ SameSite = Lax</strong> (기본값)
같은 도메인에서만 사용 가능하지만, <strong>유저가 링크를 클릭해서 접속하거나 하는 경우</strong>에는 <strong>다른 도메인에서도 사용 가능</strong>하다!
대부분의 CSRF 공격을 차단하고, 일반적인 로그인 유지에 적합해서 요즘 가장 많이 쓰이는 옵션이다.</p>
<p><strong>3️⃣ SameSite = None</strong>
다른 도메인에서도 사용 가능하며, 모든 요청에 쿠키를 전송한다. 그래서 OAuth, 서브도메인, 외부 인증에서 사용 가능하다.
ex) auth.google.com -&gt; wayout.kr(리다이렉트) 와 같은 경우에 사용할 수 있다!</p>
<h3 id="반드시️">반드시‼️</h3>
<blockquote>
<p><strong><code>Secure = True</code></strong>와 함께 써야 한다. (Secure가 없으면 브라우저가 쿠키를 아예 거부한다.)
<code>SameSite = None</code>은 사실상 CSRF 방어를 포기하는 선택이라서 브라우저가 <strong>암호화된 HTTPS 환경에서만 허용</strong>하도록 강제한다..!</p>
</blockquote>
<hr />
<p>쿠키 기반 인증은 편하지만, 옵션 없이 쓰는 쿠키 인증은 위험하다.
<code>HttpOnly</code>/<code>Secure</code>/<code>SameSite</code>는 쿠키를 제대로 쓰기 위한 최소한의 안전장치 같은 거라서 꼭 활용하도록 해야겟슨.</p>
<p>마무리는 어젯밤에 먹은 초코칩쿠키사진이다
<img alt="" src="https://velog.velcdn.com/images/dev-joohee/post/4ad039f2-0309-4528-b805-43eb76c948d4/image.jpeg" /></p>
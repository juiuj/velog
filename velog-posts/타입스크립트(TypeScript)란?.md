<h4 id="자바스크립트에-타입을-부여한-언어"><em>자바스크립트에 &quot;타입&quot;을 부여한 언어</em></h4>
<pre><code>// TypeScript
const message: string = 'hi';

function sum(a: number, b: number): number {
    return a+b;
}</code></pre><p>a: number와 b: number: 두 개의 매개변수 a와 b는 모두 숫자(number) 타입으로 명시되어있음. 
즉, 이 함수는 숫자 두 개를 입력받아야함.
<strong><em>: number</em></strong> 부분은 함수의 반환값이 숫자 타입이어야 한다는 것을 나타냄.
return a + b: 두 매개변수 a와 b를 더한 값을 반환함. 이 연산 결과도 숫자이므로 함수의 반환 타입 조건을 만족함.</p>
<h2 id="타입스크립트를-사용하는-이유"><em>타입스크립트를 사용하는 이유?</em></h2>
<ol>
<li>사용자 경험: 실행 시점(컴파일 시점)의 에러를 어느정도 미리 잡아줌</li>
<li>개발자 경험: 코드 자동 완성, 코드 역할에 대한 정보 제공 등</li>
</ol>
<h3 id="사용자-경험_-에러의-사전-방지">사용자 경험_ 에러의 사전 방지</h3>
<pre><code>// @ts-check
/**
@param {number} a
@param {number} b
@returns
*/

function sum (a,b){
    return a+b;
}
sum (10, '20') // '20' 문자열은 number에 해당하지 않음</code></pre><p>이러한 이유로 코드레벨에서 에러 사전 방지가 가능하다는 장점이 있음
=&gt; 에러 해결 시 문제 없이 잘 작동함!</p>
<p>.js 파일을 .ts 파일로 변환한다면?</p>
<pre><code>function sum (a: number, b: number){
    return a+b;
}
sum (10, '20') // 잘못된 부분을 바로 파악할 수 있음</code></pre><h3 id="개발자-경험-코드-자동-완성-코드-역할에-대한-정보-제공-등">개발자 경험: 코드 자동 완성, 코드 역할에 대한 정보 제공 등</h3>
<ul>
<li>코드를 작성할 때 개발 툴의 기능을 최대로 활용할 수 있음.<pre><code>  - 타입이 지정되어 있기 때문에 Vscode에서 해당 타입에 대한 API를 미리보기로 띄워줄 수 있고, tab으로 빠르고 정확하게 작성할 수 있음.</code></pre></li>
</ul>
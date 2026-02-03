<h2 id="구조적-타이핑이란">구조적 타이핑이란?</h2>
<h3 id="구조적-타이핑--구조적-타입-시스템structural-type-system">구조적 타이핑 = 구조적 타입 시스템(Structural Type System)</h3>
<p>객체나 데이터 타입을 정의할 때, 그 <strong>구조(멤버, 필드, 메서드 등)에 기반하여 타입을 결정</strong>하는 개념으로, 객체가 특정 타입을 따르기 위해서 <strong>명시적으로 그 타입을 선언할 필요가 없음.</strong>
대신 해당 객체가 그 타입의 구조를 충족하면 해당 타입으로 간주함.</p>
<p>≠ <strong>명목적 타입 시스템(Nominal Type System)</strong></p>
<p>구조적 타이핑에서는 객체의 이름보다는 객체가 갖고 있는 <code>속성</code>과 <code>메서드</code>가 중요함</p>
<pre><code class="language-typescript">interface Person {
    name: string;
    age: number;
}

let person = { name: &quot;Alice&quot;, age: 25 };
let anotherPerson: Person = person;  // 구조만 같으면 할당 가능
</code></pre>
<p>위의 예제에서는 <code>anotherPerson</code> 변수가 <code>Person</code> 타입으로 선언되었지만, <code>Person</code> 변수는 명시적으로 <code>Person</code> 타입으로 선언되지 않았음.
그러나 <code>person</code> 객체가 <code>Person</code> 타입의 구조를 만족하기 때문에 타입 추론에 의해 <code>anotherPerson</code> 변수에 할당될 수 있음.</p>
<p><strong>즉, 객체의 구조만 맞으면 해당 타입으로 간주됨</strong></p>
<p>Q.<span style="color: red;">구조적 타이핑의 장점은?</span>
A. <del><span style="color: gray;">객체가 특정 클래스를 명시적으로 상속받거나 구현하지 않더라도 구조만 맞으면 그 타입으로 사용할 수 있어서 유연하게 코드를 작성할 수 있다.
또한 간결한 코드 작성이 가능하다.</span></del></p>

# 코드스피츠 86 갹채자형 자바스크립트- 1강  

## Value Context vs Identifier Context
:Context 관점

> Value Context : 값을 기반으로 하는 컨텍스트는 메모리의 주소는 상관없이 값이 같으면 같다고 판단하는 것.
> Identifier Context : 식별자 기반으로 하는 컨텍스트는 힙메모리에 있는 객체를 두 변수가 가르키는 객체의 주소가 같으면 같다고 판단하는 것.

두 관점의 따라 프로그래밍의 기법이 달라지는데,
Value Context 를 함수형 프로그래밍에서 사용하며, Identifier Context 는 객체지향 프로그래밍에서 사용한다.
프로그래밍에서는 하나의 컨텍스트만 가지고 프로그래밍하는 것이 중요하다.
Value 와 Identifier 를 혼동해서 사용하는 순간 버그의 가능성이 폭주하기 떄문이다.


<pre><code>
const a = {a:3,b:5};
const b = {a:3,b:5};

console.log(a === b);  -> Identifier Context 
console.log(JSON.stringify(a) === JSON.stringify(b));  -> Value Context
</code>
</pre>



# 코드스피츠 86 갹채자형 자바스크립트- 1강



## Value Context vs Identifier Context
> Context 관점

>  Value Context : 값을 기반으로 하는 컨텍스트는 메모리의 주소는 상관없이 값이 같으면 같다고 판단하는 것.
> Identifier Context : 식별자 기반으로 하는 컨텍스트는 힙메모리에 있는 객체를 두 변수가 가르키는 객체의 주소가 같으면 같다고 판단하는 것.

두 관점의 따라 프로그래밍의 기법이 달라지는데,
Value Context 를 함수형 프로그래밍에서 사용하며,
Identifier Context 는 객체지향 프로그래밍에서 사용한다. 객체지향 프로그래밍에서 Value Context 를 사용하면 객채지향이 깨진다.

프로그래밍에서는 하나의 컨텍스트만 가지고 프로그래밍하는 것이 중요하다.
Value 와 Identifier 를 혼동해서 사용하는 순간 버그의 가능성이 폭주하기 떄문이다.

<code><pre>
const a = {a:3,b:5};
const b = {a:3,b:5};

console.log(a === b);  -> Identifier Context
console.log(JSON.stringify(a) === JSON.stringify(b));  -> Value Context
</pre>
</code>

객체지향에서 가장 기본은 인자는 무조건 객체만 사용하는 것.
값을 사용하는 경우는 온리 생성자밖에 없음.

### 값의 특징
1. 끝 없이 복사본
2. 상태 변화에 안전? -> 안전해보일뿐..
3. 연산을 기반으로 로직전개

### 식별자의 특징
1. 하나의 원본
2. 상태 변화를 내부에서 책임짐
3. 메시지를 기반으로 로직 전개

## 본론
객체지향에서 제일 중요한것은 값을 사용하지 않는 것.
객체지향의 가장 중요한 성질
# Polymorphism(폴리모피즘) : 다형성

<code>
<pre>
class Worker = class {
    run(){
        console.log("working")
    }
    print(){
        this.run()
    }
}

const HardWorker = class extends Worker{
    run(){
        console.log("HardWorker")
    }
}
const worker = new HardWorker();
console.log(worker instanceof Worker);  -> 대체가능성
worker.print();  -> 내적일관성
</pre>
</code>

# Substitution & Internal identity
폴리모피즘의 대체가능성 (substitution)
-> 확장(자식)클래스가 대상(부모)클래스로 대체할 수 있다.
폴리모피즘의 내적일관성 (internal identity)
-> 생성된 클래스의 본질은 유지된다.

Polymorphism of Prototype










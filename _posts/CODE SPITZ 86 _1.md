# 코드스피츠 86 갹채자형 자바스크립트- 1강


## Value Context vs Identifier Context
> Value Context : 값을 기반으로 하는 컨텍스트는 메모리의 주소는 상관없이 값이 같으면 같다고 판단하는 것.
> Identifier Context : 식별자 기반으로 하는 컨텍스트는 힙메모리에 있는 객체를 두 변수가 가르키는 객체의 주소가 같으면 같다고 판단하는 것.


프로그래밍에서는 하나의 컨텍스트(관점)만 가지고 프로그래밍하는 것이 중요하다.
어느 관점이냐에 따라 프로그래밍의 기법이 달라지는데, Value Context는 함수형 프로그래밍에서 사용하며, 
Identifier Context 는 객체지향 프로그래밍에서 사용한다. 
객체지향 프로그래밍의 가장 기본은 Value Context를 사용하지 않는것이며 사용하는순간 객체지향이 깨진다고 볼 수 있다.
Value 와 Identifier 를 혼동해서 사용하는 순간 버그의 가능성이 폭주하기 떄문이다.
객체지향에서 값을 사용하는 경우는 생성자 밖에 없어야한다.

###### Identifier Context와 Value Context 코드예제
<code><pre>
const a = {a:3,b:5};
const b = {a:3,b:5};

console.log(a === b);  -> Identifier Context
console.log(JSON.stringify(a) === JSON.stringify(b));  -> Value Context
</pre>
</code>


### 값의 특징
1. 끝 없이 복사본
2. 상태 변화에 안전? -> 안전해보일뿐..
3. 연산을 기반으로 로직전개

### 식별자의 특징
1. 하나의 원본
2. 상태 변화를 내부에서 책임짐
3. 메시지를 기반으로 로직 전개


# Polymorphism(폴리모피즘) : 다형성
>폴리모피즘이랑 객체지향에서 가장 중요한 성질이다.

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

위의 코드를 보면 worker객체는 HardWorder로부터 생성되었다. 
그런데 instanceof Worker를 했을때 true가 나온다. 



# Substitution & Internal identity
> substitution : 폴리모피즘의 대체가능성   
>> 확장(자식)클래스가 대상(부모)클래스로 대체할 수 있다.    

> internal identity : 폴리모피즘의 내적일관성   
>> 생성된 클래스의 본질은 유지된다.   

# Polymorphism of Prototype
함수나 클래스에는 속성으로 Prototype 이라는 객체를 가지게 된다.
새로 생성된 객체에는 __proto__가 생성된다.
Prototype 도 객체기 때문에 __proto__가 생성된다.
함수의 Prototype 객체에는 constructor 속성이 존재한다.
constructor 는 자기 자신의 함수를 가르킨다.
__proto__는 부모 클래스의 Prototype 을 가르킨다.

자기가 찾는 메소드이름이나 속성이름을 자기자신의 __proto__에서 찾아보고 없으면 가까운 Prototype 을 타고가서 찾아보고 또 없으면 타고타고 올라가,
상속 구조로 Prototype Chain 구조를 가지게 된다.

### 자바스크립트에서 내적일관성을 구현하는 방법
JS에서는 이렇게 가장 가까운 자기 자신의 Prototype 을 먼저 찾게되어 내적일관성을 달성하게 된다.
### 자바스크립트에서 대체가능성을 구현하는 방법
A instanceof B
A에 __proto__와 __proto__가 가르키는 Prototype -> constructor 가 B인지 비교한다. 
null 이 나올때까지 prototype chain 을 타고 올라가서 비교한다.

# Object essentials
객체지향의 언어에 조건을 만족했다고 객체지향프로그래밍이라고 할 수 없다.
본질적인 측면으로 무엇이 있느냐,

> Maintenance of State : 상태 관리 책임   
> Encapsulation of Functionality : 기능의 캡슐화

> ##Isolation of change : 변화에 대한 격리

<code><pre>
const EssentialObject = class{
    #name = "";  -> hide state
    #screen = null;
    constructor(name){
        this.#name = name;
    }
    camouflage(){
        this.#screen = (Math.random() * 10).toString(16).replace(".", """"")
    }
    get name(){
        return this.#screen || this.#name;  -> encapsulation
    }
};
</pre></code>



#알려진 기본 설계요령
##객체지향 원칙
###SOLID원칙
1. SRP (Single Responsibility) 단일책임
-> 하나의 책임만 가진다.(코드 수정원인이 하나만 되도록 한다.)
-> 지키지 못하면 산탄총 수술(shotgun surgery)이 발생한다.
2. OCP (Open Closed) 개방폐쇄 원칙
-> extends, implement 의 확장이 가능하도록 하고 
수정이 필요해도 해당 코드를 수정하지말고 새로운 객체를 만들어서 확장하라.
3. LSP (Liskov Substitution) 업캐스팅 안전
-> 추상층의 정의가 너무 구체적이면 구상층의 구현에 모순이 발생함.
-> LSP가 성립되지 않으면 ISP로 해결할 수 있다. 
4. ISP (interface Segregation) 인터페이스분리
-> 
5. DIP (Dependency Inversion) 다운캐스팅 금지
-> SOLID원칙이 모두 지켜져야만 DIP가 지켜진다.

###DI (Dependency Injection) 의존성주입 
> IoC (Inversion of Control) 제어역전의 구현체 중 하나

###DRY (Don`t Repeat Yourself) 중복방지 
###Hollywood Principle 의존성 부패방지
->물어보지말고 시켜라.
->캡슐화가 가능해진다.
###Law of demeter 최소 지식
->최소한의 지식으로만 메소드나 객체를 만들어야한다.
->너무 많이 알면 의조성 부패
->지켜지지않으면 열차전복사고가 발생한다. (train wreck)
->classA.methodA의 최대 지식 한계
    1. 인자로 넘어온 객체 
    2. methodA에서 생성된 객체 
    3. classA가 가지고 있는 필드 객체
    
    
#Message
>단일 책임 원칙을 준수하는 객체망이 책임이상의 업무를 부여받으면 
메세지를 이용하여 다른객체에서 의뢰하여 문제를 해결하도록 해야한다.

1. 메세지 - 의뢰할 내용
2. 오퍼레이션 - 메시지를 수신할 개체가 제공하는 서비스 
-> worker.run() 처럼 실행메소드를 실제 처리기에 연결해주는 역할.
3. 메소드 - 오퍼레이션이 연결될 실제 처리기

#Dependency
-> 객체망을 이용하여 설계가 이루어지지만 객체의 의존성으로 인해 의존성문제가 발생되는 모순이 있다.
의존성이 많아도 , 적어도 문제가 발생한다. 그것이 디자인설계가 어려운 이유이다....
 
##종류
1. 개체의 생명 주기 전체에 걸친 의존성
객체의 생성부터 제거될때까지 영구적으로 연결되기때문에 변화에 크리티컬한 문제가 생긴다.
- 상속 (extends) : 부모객체와 자식객체가 합쳐져있기 떄문에 변화에 취약하다. 
- 연관 (association) : 필드에 객체 타입을 알고 있다.
2. 오퍼레이션 실행 시 임시적인 의존성
- 의존 (dependency) : 메소드 단위로만 오퍼레이션 실행시에만 의존성이 생긴다. 

= 상속 > 연관 > 의존 순으로 의존성이 약해진다.

##의존성이 높으면 생기는 현상 
1. 수정의 여파가 증가되며 
2. 수정하기 어려운 구조 생성된다.
3. 순환 의존성 (한 뭉떵이가 돼버린다.)


##Dependency Inversion
어떠한 경우에도 다운캐스팅은 금지하고 폴리모피즘(추상인터페이스) 사용



 











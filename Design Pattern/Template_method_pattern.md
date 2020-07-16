#템플릿 메소드 패턴 (Template method pattern)
- 템플릿을 만들어주고 특정 메서드 안을 채워 넣는 디자인 패턴
- 여러 클래스에서 공통으로 사용하는 메서드를 상위클래스에서 정의하고
하위 클래스 각각에서 다르게 구현되는 메서드만 각자 구현하는 패턴을 의미
> A->B->C->D 메소드로 구동되는 클래스에서 B 메소드가 하위클래스에 따라 내용이 달라질 때
A, C, D는 상위클래스에서 정의하고 B 메소드만 하위클래스에서 구현한다. 

> 이때 하위클래스에서 구현해야 하는 B 메소드를 훅(hook) 이라고 합니다.

```
public class Parent {
    public void methodA() {
        sout("Method-A");
    }
    public void methodB() {

    }
    public void methodC() {
        sout("Method-C");
    }
    public void methodD() {
        sout("Method-D");
    }
    public method() {
        methodA();
        methodB();
        methodC();
        methodD();
    }
}
```
```
public class ChildA extends Parent {
    @Override
    public void methodB() {
        sout("ChildA's method-B");
    }
}

public class ChildB extends Parent {
    @Override
    public void methodB() {
        sout("ChildB's method-B);
    }
}
```
```
public class Main {
    public static void main(String[] args) {
        ChildA = childA = new ChildA();
        ChildB = childB = new ChildB();

        childA.method();
        childB.method();
```
# 전략 패턴 (Strategy pattern)
- 객체마다 다를 수 있는 메서드를 캡슐화해 교환하여 사용하는 디자인 패턴
1. 객체들이 할 수 있는 메서드 (행위) 각각에 대해 전략 클래스를 생성한다.
2. 유사한 행위들을 캡슐화하는 인터페이스를 정의한다.
3. 객체의 행위를 바꾸려고 할 때 직접 행위 인터페이스를 수정하는 것이 아닌
전략을 바꾸어주기만 한다.
> 객체가 할 수 있는 메서드들이 각각의 전략으로 생성되어 객체의 행위가 수정될 때 
> 객체에 할당되어있는 행위 자체를 수정하는 것이 아닌 할당된 전략을 
> 수정된 전략으로 바꾸는 것을 말합니다.

### 전략패턴을 사용하지 않았을 때 :
A 자동차 회사와 B 자동차 회사가 존재할 때:  

A 자동차 : 2기통 엔진으로 구동한다.  
B 자동차 : 4기통 엔진으로 구동한다.  

```
public interface Vehicle {
    publice void engine();
}
```
```
public class ACar implements Vehicle {
    public void engine() {
        sout("2기통 엔진으로 구동합니다");
    }
}

public class BCar implements Vehicle {
    public void engine() {
        sout("4기통 엔진으로 구동합니다");
    }
}
```
```
public class Client {
    public static void main(String[] args) {
        Vehicle aCar = new ACar();
        Vehicle bCar = new BCar();
        aCar.engine();
        bCar.engine();
```
위의 코드에서 만약 A 자동차의 엔진이 4기통으로 변경되었을 때 ACar 클래스의 engine()
메소드의 내용을 바꾸어준다면 해결이 됩니다.

```
public class ACar implements Vehicle {
    public void engine() {
        sout("4기통 엔진으로 구동합니다");
    }
}
```
하지만 이렇게 수정을 한다면 메서드의 내용 자체를 수정하였기 때문에 
**Open-Closed Principle**에 위배됩니다.  
그리고 객체들끼리 engine() 메서드 중복이 발생합니다.

### 전략 패턴 사용 방법
1.위의 설명과 같이 객체들이 할 수 있는 메서드들에 대한 전략 클래스를 작성합니다.  
그리고 엔진에 관한 전략들이니 모아서 캡슐화를 진행해줍니다.

```
public interface EngineStrategy {
    public void engine();
}
```
```
public class V2Engine implements EngineStrategy {
    public void engine() {
        sout("2기통 엔진으로 구동합니다");
    }
}
public class V4Engine implements EngineStrategy {
    public void engine() {
        sout("4기통 엔진으로 구동합니다");
    }
}
```

2.이제 자동차에 대한 클래스를 정의합니다.  
engine() 메소드를 통하여 엔진을 확인할 수 있는데 자동차 클래스 내에 직접 구현하지 않고
구동하는 엔진의 전략을 설정하고 그 전략을 사용하도록 합니다.
```
public class Engine {
    private EngineStrategy engineStrategy;
    public void engine() {
        engineStrategy.engine();
    }

    public void setEngineStrategy(EngineStrategy inputEngineStrategy) {
        this.engineStrategy = inputEngineStrategy;
    }
}
```
```
public class ACar extends Engine {
}
public class BCar extends Engine {
}
```

3.사용하는 메인 클래스를 작성합니다.
```
public class Client {
    public static void main(String[] args) {
        Engine aCar = new ACar();
        Engine bCar = new BCar();

        aCar.setEngineStrategy(new V2Engine);
        bCar.setEngineStrategy(new V4Engine);

        aCar.engine();
        bCar.engine();
        
        aCar.setEngineStrategy(new V4Engine);
        aCar.engine();
    }
}
```
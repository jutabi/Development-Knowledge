# Dependency Inversion Principle
- 의존성 부패 (Dependency Rot) (A 클래스가 B 클래스를 의존하여 재사용하지 못할 때)가 일어날 때 사용한다.
- 전략패턴과 유사한 구조이지만 다름

### 적용하기 전의 의존성 부패
```
public class Button {
    Engine engine = new Engine();
    boolean isOn = false;

    public void toggle() {
        isOn = !isOn;
        if (isOn) {
            engine.stop();
        } else {
            engine.start();
        }
    }
}

public class Engine {
    public void start() {
        sout("engine is started");
    }
    public void stop() {
        sout("engine is stoped");
    }
}
```
- 위의 코드에서 Button 클래스는 Engine 클래스를 의존하는 관계를 가진다.  
(Button 클래스가 Engine 객체를 생성하여 사용하며, Engine 클래스가 변경되면 Button 클래스에 영향을 끼친다.)
- Engine 클래스만 재사용이 가능하며 Button 클래스는 Engine 클래스 이외에 AC 를 켜고 끄는 클래스로 재사용할 수 없다.
- 이러한 이유들로 인해서 DIP 를 사용한다.

### DIP의 적용
```
public class Button {
    private ISwitchButton switch;

    public Button(ISwitchButton swi) {
        this.switch = swi;
    }

    public void toggle() {
        isOn = !isOn;
        if (isOn) {
            switch.stop();
        } else {
            switch.start();
        }
    }
}

public interface ISwitchButton {
    public void start();
    public void stop();
}

public class Engine implements ISwitchButton {
    ...
    public void start() {
        sout("Engine is started");
    }
    public void stop() {
        sout("Engine is stoped");
    }
}
public class AC implements ISwitchButton {
    ...
    public void start() {
        sout("AC is started"):
    }
    public void stop() {
        sout("AC is stoped");
    }
}
```
- 위의 코드와 같이 Button 클래스가 Engine, AC 클래스를 직접 의존(참조)하는 것이 아니라
인터페이스를 참조하게 하고 구현체에서 start(), stop() 메소드를 구현하게 하여 Engine 클래스와 AC 클래스
모두 다 사용하게 하는 재사용성을 만족시킨다.
- 처음에 전략패턴과 유사한 구조라고 설명을 하였는데 다른점을 아래에서 설명한다.
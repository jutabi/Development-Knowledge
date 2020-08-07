# 스테이트 패턴 (State pattern)
- 전략 패턴과 유사한 구조를 가진다.
- 객체의 특정 상태들을 객체화 하여 그 상태일 때 할 수 있는 메소드를 각각 작성한다.
- 그리고 여러가지 상태들을 인터페이스로 캡슐화 하여 사용할 때 인터페이스를 호출한다.

### 스테이트 패턴 예시
- 자동차의 상태가 시동 꺼짐(OFF), ACC, 시동 켜짐(ON) 상태가 존재할 때
- 자동차의 기본 상태는 시동 꺼짐
- 운전자가 시동이 꺼진 상태에서 Start 버튼을 누르면 ACC 상태가 되고
- 운전자가 브레이크를 밟고 Start 버튼을 누르면 시동이 켜지고
- 운전자가 시동이 켜진 상태에서 Start 버튼을 누르면 시동이 꺼진다

#### 스테이트 패턴을 적용하지 않았을 때:
```
public class Car {
    private String state = "";

    public Car() {
        setState("OFF");
    }

    public void setState(String inputState) {
        this.state = inputState;
    }
    
    public void start_button(boolean brake) {
        if (this.state.equals("OFF") {
            if (brake) {
                setState("ON");
            } else {
                setState("ACC");
            }
        } else {
            setState("OFF");
        }
    } 
}
```
위와 같은 코드로 구현이 가능하다.  
  
하지만 위의 상태만으로도 조건문이 복잡해지기 시작하고,  
만약 시동이 걸린 상태에서 기어를 바꾸는 버튼을 눌렀을떄 P R N D 의 경우를 가진 **기어 상태까지 추가**된다면
조건문은 더욱더 복잡해져 파악하기 쉽지 않고 Car 클래스를 직접 수정해야하는 일이 생기게 된다.
  
그렇기 때문에 상태 패턴을 사용한다.

#### 상태 패턴 적용:
```
public class Car {
    private State state;
        
    public Car() {
        state = OffState.get();
    }
    public void setState(State state) {
        this.state = state;
    }

    public void startButton(boolean brake) {
        this.state.startButton(this, brake);
    }
}
```
- Car 클래스 안의 조건문을 밖으로 빼고 상태들 (ON, ACC, OFF)을 캡슐화 시켜준다.
- 위의 Car 클래스에서 startButton() 메소드로 상태를 변경을 위임할 때 자신을 (this)를 전달한다.
```
public interface State {
    public void startButton(Car car, boolean brake);
}
```
- 각각의 상태들이 클래스가 되어 구현되었다. 
- 상태가 여러번 변할 것이기에 싱글톤으로 구현하여 메모리 낭비를 방지한다.
```
public class OnState inplements State {
    private OnState() { }

    private static class LazyHolder {
        public static final OnState ON = new OnState();
    }
    public static OnState get() {
        return LazyHolder.ON;
    }
    
    @Override
    public void startButton(Car car, boolean brake) {
        car.setState(OffState.get());
    }
}

public class OffState implements State {
    private OffState() { }

    private static class LazyHolder {
        public static final OffState OFF = new OffState();
    }
    public static OffState get() {
        return LazyHolder.OFF;
    }

    @Override
    public void startButton(Car car, boolean brake) {
        if (brake) {
            car.setState(OnState.get());
        } else {
            car.setState(AccState.get());
        }
    }
}

public class AccState implements State {
    private AccState() { }

    private static class LazyHolder {
        public static final AccState ACC = new AccState();
    }
    public static AccState get() {
        return LazyHolder.ACC;
    }

    @Override
    public void startButton(Car car, boolean brake) {
        if (brake) {
            car.setState(OnState.get());
        } else {
            car.setState(OffState.get());
        }
    }
}
```
```
public class Main {
    public static void main(String[] args) {
        Car car = new Car();

        car.startButton(false);
        car.startButton(true);
        car.startButton(false);
    }
}
```
#### 전략패턴과의 차이점
- 전략 패턴은 아래처럼 setter 를 이용하여 **사용자가 직접 수행할 전략을 주입**해준다.
- 사용자가 클래스가 할 수 있는 전략들에 무엇이 있는지 아는 것이다.
```
aCar.setEngineStrategy(new V2Engine);
bCar.setEngineStrategy(new V4Engine);

aCar.engine();
bCar.engine();

aCar.setEngineStrategy(new V4Engine);
aCar.engine();
```
- 하지만 상태 패턴은 **상태를 정하는 setter 가 존재하지 않고** 버튼을 누르는 메소드 하나만으로
상태 클래스 안에서 알아서 처리한다는 점에서 전략패턴과의 차이가 있다.
> 브레이크를 입력하는 것은 상태로 치지 않는다는 가정하에
```
car.startButton(false);
car.startButton(true);
car.startButton(false);
```
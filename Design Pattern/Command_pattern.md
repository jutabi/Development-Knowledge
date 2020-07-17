# 커맨드 패턴 (Command pattern)
- 사용자가 A 클래스를 통해 B 클래스나 C 클래스를 제어하거나 내장 메서드를 실행하려고 할 때
사용하는 디자인 패턴
- A 클래스의 한 메소드가 B 클래스와 C 클래스 둘다 제어, 실행 할 수 있을때 사용한다.
- 커맨드(제어)할 클래스를 정하고 (set()) 제어 메소드를 실행한다.
- ex) 자동차의 엑셀을 밟았을 때  
  - 전진 기어(D) 라면: 차를 앞으로 전진한다.
  - 후진 기어(R) 라면: 차를 뒤로 후진한다.  
  - 엑셀 클래스의 stepOn() 메소드가 전진 클래스와 후진 클래스 둘다 제어, 실행할 수 있다.
  
#### 커맨드 패턴을 사용하지 않았을 때 :
```
public class Forward {
    public void accel() {
        sout("전진");
    }
}
public class Backward {
    public void accel() {
        sout("후진");
    }
}
```
```
public class Accelerator {
    private Forward forward;
    private Backward backward;

    public Accelerator(Forward forward, Backward backward) {
        this.forward = forward;
        this.backward = backward;
    }

    public void acceleration(String inputGear) {
        if (inputGear.equals("D") {
            this.forward.accel();
        } else if (inputGear.equals("R") {
            this.backward.accel();
        }
    }
}
```
```
public class Driver {
    public static void main(String[] args) {
        Forward forward = new Forward();
        Backward backward = new Backward();
        Accelerator acc = new Accelerator(forward, backward);

        acc.acceleration("D");
        acc.acceleration("R");
```
- 위와 같은 코드가 커맨드 패턴을 사용하지 않았을 때입니다.  
- D와 R 이외에도 P, N 기어의 accelerator 기능이 추가된다면
accelerator 의 분기가 더욱더 늘어나고, 현재도 OCP 에 위반됩니다.  
- 그래서 커맨드 패턴을 사용합니다.  
  - A 클래스가 B, C 클래스 이외에 더 많은 클래스를 제어하더라도 의존성을 제거 할 수 있도록 합니다.
  
#### 커맨드 패턴 적용
- 제어할 수 있는 commands 캡슐화
```
public interface Command {
    public void accel();
}

public class Forward {
    public void accel() {
        sout("전진");
    }
}
public class ForwardCommand implements Command {
    private Forward forward;

    public ForwardCommand(Forward forward) {
        this.forward = forward;
    }
    public void accel() {
        forward.accel();
    }
}

public class Backward {
    public void accel() {
        sout("후진");
    }
}
public class BackwardCommand implements Command {
    private Backward backward;

    public BackwardCommand(Backward backward);
        this.backward = backward;
    }
    public void accel() {
        backward.accel();
    }
}
```
- Accelerator 수정
```
public class Accelerator {
    private Command command;

    public setCommand(Command command) {
        this.command = command;
    }
    public void accel() {
        command.accel();
    }
}
```
- Driver 수정
```
public class Driver {
    public static void main(String[] args) {
        Forward forward = new Forward;
        ForwardCommand forwardCommand = new ForwardCommand(forward);

        Backward backward = new Backward;
        BackwardCommand backwardCommand = new BackwardCommadn(backward);

        Accelerator acc = new Acceleractor();

        acc.setCommand(forwardCommand);
        acc.accel();

        acc.setCommand(backwardCommand);
        acc.accel();        
```
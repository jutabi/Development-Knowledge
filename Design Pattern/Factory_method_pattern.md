# 팩토리 메서드 패턴 (Factory method pattern)
- 상황, 조건에 따라 객체를 다르게 생성해야 할 때 사용하는 패턴
- 메인 클래스 내의 조건문 분기를 통한 객체생성이 아닌 팩토리 클래스에게 객체 생성을 위임하는 방식

```
public abstract class Car {

}

public class ACar extends Car {
    ...
}
public class BCar extends Car {
    ...
}
public class CCar extends Car {
    ...
}
```
```
public class CarFactory {
    public Car createCar(String type) {
        Car car = null;
        if (type.equals("A") {
            car = new ACar();
        }
        else if (type.equals("B") {
            car = new BCar();
        }
        else if (type.equals("C") {
            car = new CCar();
        }
    return car;
}

public class MakeCar1 {
    public Car createCar(String type) {
        CarFactory factory = new CarFactory();
        Car car = factory.createCar(type);

        return car;
    }
}

public class MakeCar2 {
    public Car createCar(String type) {
        CarFactory factory = new CarFactory();
        Car car = factory.createCar(type);

        return car;
    }
}
```

- 위의 코드처럼 작성하는 것을 팩토리 메소드 패턴이라고 합니다.  
- MakeCar 클래스가 한개만 있다면 MakeCar 클래스 내에 분기문을 작성해도 되지만
차를 만드는 클래스가 2개 이상부터는 코드의 중복이 생기고 클래스간의 결합도가 높아집니다.
- 그래서 객체를 생성하는 팩토리 클래스를 생성하고 그 팩토리 클래스로 여러 클래스에서
객체 생성을 위임합니다.
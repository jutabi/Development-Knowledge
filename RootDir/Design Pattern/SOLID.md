# SOLID 원칙
## 1. SRP (Single Responsibility Principle)
- 객체는 단 하나의 책임만 가져야 한다는 원칙
- 계산기는 사칙연산을 제외한 다른 기능은 가지고 있지 않아야 한다.
- 그리고 각 기능들 +, -, *, / 는 각각의 함수로 정의되어 있어야 한다.
## 2. OCP (Open Closed Principle)
- 개방 폐쇄 원칙
- 기능을 추가하는데 있어서는 열려있고,  
기존 코드 변경에는 닫혀있음의 원칙
> 확장에 대해선 개방되어 있고 수정에 대해선 폐쇄되어야 한다는 의미
- 인터페이스를 통해 **캡슐화**하는 방법을 사용한다.
## 3. LSP (Liskov Substitution Principle)
- 자식 클래스는 최소한 자신의 부모 클래스에서 가능한 행위를 수행할 수 있어야 한다.
> 어떠한 로직에서 부모 클래스 대신에 자식 클래스 객체를 대체하여 삽입해도 동작하여야 한다.  
> (로직의 의미가 변경되지 않아야 한다.) -> 일관성
- 일관성을 지키기 위해선 자식 클래스에서의 오버라이드를 수행하지 않아야 한다.
- 추가되는 기능은 새로운 메소드를 자식 클래스 내에서 정의하고 오버라이드 하더라도 확장의 개념으로 사용
## 4. ISP (Interface Segregation Principle)
- 사용하지 않는 인터페이스는 구현하지 않도록 한다.
> 여러 기능들을 포함하는 인터페이스에서 상속받는 자식 클래스들이 전체 기능을 다 사용하지 않고
특정 기능만을 사용할 경우 기능별로 인터페이스를 분리한다.
- 예를들어 소리에 관련한 인터페이스가 있다고 하면 DAC, ADC, 출력 변경 등등의 여러 기능들이 
상속되었을 때 DAC, ADC, 출력 변경 등의 자식클래스들이 상속받아 하나의(특정) 기능만 사용할 경우
DAC, ADC, 출력 변경의 인터페이스를 따로 구현한다.

- 변경전
```
interface Sound {
    dAC() { }
    aDC() { }
    output_Ch() { }
}

class DAC implements Sound {
    @Override
    dAC() { ... }
}

class ADC ...
```
- 변경후
```
interface IDAC() {
    dAC() { }
}

class DAC implements IDAC() {
    @Override
    dAC() { ... }
}
```
## 5. [DSP (Dependency Inversion Principle)](SOLID/Dependency_inversion_principle.md)
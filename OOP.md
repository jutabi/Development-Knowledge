# OOP (Object Oriented Programming)

#### 객체 지향 프로그래밍이란
> 프로그래밍에서 필요한 데이터를 추상화하여 상태와 행위를 가진 객체를 만들고
여러 객체들간의 상호작용을 통해 로직을 구성하는 프로그래밍 패러다임

#### 기본적인 틀
```
class Animal {
    age = 0
    satiety = 0

    def eat(food)
        satiety += food.calorie
    end
}
```

## 구성 요소
- 클래스 (Class) (-> class Animal )
    - 같은 종류의 집단에 속하는 속성(attribute)과 행위(behavior)를 정의한 것
- 객체 (Object) (-> ani = Animal.new() )
    - 클래스를 이용하여 실제 메모리에 할당(생성)한 것
    - 클래스 내에서 정의된 속성과 행위를 사용할 수 있다.
- 메서드 (Method) (-> eat(food) )
    - 클래스로부터 생성된 객체를 사용하는 방법
    - 객체의 속성(attribute)을 조작할 수 있다.

## OOP의 장점
- 재사용성
    - 이전에 만들어진, 어떠한 기능을 가지는 클래스를 가져와 사용하거나 상속, 확장 하여 사용 가능
- 유지보수
    - 코드를 수정함에 있어 기능별로 서로 다른 클래스, 패키지 내에 있기 때문에 수정을 원하는 클래스
    에서 수정하기에 편리함.
    - 코드 직관성 (분석)
- 프로그램의 규모에 따른 업무 분담
    모듈화하여 개발함으로 담당 기능에 따른 여러 개발자들의 분업이 편리하다.

## OOP의 단점
- 처리속도
- 용량
- 믹서기에 들어가는 개발자들

## OOP의 중요 키워드
#### [1. 클래스와 객체](#구성-요소)
#### 2. 추상화
- 불필요한 정보(특성)는 숨기고 중요한 정보만을 표현하여(묶어) 프로그램을 단순화하는 것
#### 3. 캡슐화
- 데이터를 외부에서 직접 접근하게 하지 않고 함수를 통해서만 조작하도록 하는 것 (getter, setter)
- 속성과 행위를 하나로 묶는다.
- 접근지정자를 두고 getter()와 setter()을 구현한다.  
(public(+), private(-), protected(#) (기호는 UML에서의 사용법))
```
public class Monster {
    private int level = 0;
    private int hp = 0;

    public int getLevel() {
        return level;
    }
    public void setLevel(int input) {
        this.level = input;
    }

    public int getHp() {
        return hp;
    }
    public void setHp(int input) {
        this.hp = input;
    }

    public void attack() {

    }
}
```
#### 4. 상속
- 자식 클래스와 부모 클래스가 존재하고 자식 클래스는 부모 클래스의 속성과 행위를 물려받는 것을 의미한다.
```
public abstract class Monster {
    ... (위의 코드 참조)
}

public class Goblin extends Monster {
    @Override
    public void attack() {
        ...
    }
}
```
- 고블린 이외에도 다른 몬스터들이 존재할 때 그들은 공통적으로 level, hp 속성, attack() 메소드가 존재할 수 있다.  
이러한 공통된 속성과 행위를 묶어 부모 클래스로 만들고 자식클래스는 상속을 하여 사용한다.
- ##### Override
    - 자식 클래스가 부모의 기능을 물려받아 사용하는데 메소드명은 동일하지만 구현 내용은 다를 때 사용하는 방법
    - 재정의하여 사용한다고 한다.
    - 공통적으로 attack 한다는 행위는 같지만 그 안의 세부 구현 내용들이 자식클래스마다 다를 수 있기 때문에
    자식 클래스만의 고유한 attack() 메소드를 재정의 구현하여 사용한다.
- ##### + Overload
    - 상속과는 관계가 없다.
    - 메소드명이 동일하다는 점에서는 Override와 같지만 다르다.
    - 매개변수의 개수나 자료형의 차이에 따라서 메소드명은 같지만 서로 다른 메소드로 취급하는 것을 말한다.
    ```
    public class Cal {
        public int add(int a, int b) {
            return a + b;
        }
        public int add(int a, int b, int c) {
            return a + b + c;
        }
    }
    public static void main(String[] args) {
        Cal cal = new Cal();
        sout(cal.add(1, 2));
        sout(cal.add(1, 2, 3));
    }
    ```

#### 5. 다형성
- 속성(변수)이나 행위(함수)가 상호아에 따라 다른 의미로 해석될 수 있는 것

#### 6. 정보 은닉

## [OOP 5대 원칙(SOLID)](./Design%20Pattern/SOLID.md)
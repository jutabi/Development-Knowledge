# 제네릭
- 클래스 내부에서 사용할 데이터 타입을 외부에서
(클래스의 인스턴스를 생성할 때) 지정하는 기법
- JDK1.5부터 도입됨

## 사용 예시
```
public class AClass<T> {
    private T input;

    public void set(T input) {
        this.input = input;
    }
    public T get() {
        return input;
    }
}

public class Main() {
    public static void main(String[] args) {
        AClass<Integer> intValue = new AClass<Integer>();
        ACalss<String> stringValue = new AClass<String>();

        intValue.set(10);
        //intValue.set("10); -> 에러 발생

        stringValue.set("10");
        //stringValue.set(10); -> 에러 발생

        sout(intValue.get());
        sout(stringValue.get());
    }
}
```
1. AClass의 인스턴스를 생성할 때 <>안에 사용할 타입을 설정해주었다.
2. Integer를 사용하여 생성하면 객체가 생성될 때 T가 Integer로 바뀌어 객체가 생성된다.
    > 제네릭은 참조형 데이터 타입만이 설정 가능한데 'int'는 기본형 데이터 타입임으로 래퍼 클래스인 Integer를 사용한다.
3. intValue 객체의 input 변수가 int형으로 선언된다.

## 제네릭을 사용하는 이유
- 위와 같은 제네릭을 사용하는 방식은 어딘가 쓸모가 있어보인다. 왜 사용할까?
#### 1. 에러체크
- 컴파일시에 타입을 체크하여 에러를 찾기에 쉽다
#### 2. 타입캐스팅
- 컴파일시에 자동으로 형변환이 이루어진다.
#### 3. 코드 재사용성
- 위의 예제와 같이 기능은 동일하지만 자료형만 다를 때 코드를 재사용하기에 좋습니다.

## + 자료형 한정하기 (한정적 타입 매개변수 (Bounded Type Parameter))
- 제네릭으로 사용할 자료형을 한정할 수 있는 방법
```
public class AClass<T extends Number> { ... }
```
- AClass의 제네릭으로 들어오는 자료형을 Number의 서브 클래스로 한정한다.  
(ex) Byte, Short, Integer, Long, Double)
- 상위클래스로 한정하고 싶은 경우 'super'를 사용한다.
```
public class AClass<T super ***>
```

## + 복수 제네릭
- 복수개의 제네릭을 사용하는 것도 가능하다.
```
public class AClass<T, K> { ... }
```
- Java의 HashMap이 그 예
```
HashMap<String, Integer> map = new HashMap<String, Integer>();
```

## + 제네릭 메서드
- 반환값의 자료형과 매개변수의 자료형으로 T를 갖는 메소드
- 제네릭 클래스 이외의 일반 클래스 내부에도 정의할 수 있다.
- 리턴타입을 정의하기 전에 제네릭 메소드라는 것을 명시하기 위해 제네릭 타입에 대한 정의를 해야한다.
```
public static <T> T methodA(T input) { ... }
```
```
public static <T extends Number> void methodB(T input) { ... }
```
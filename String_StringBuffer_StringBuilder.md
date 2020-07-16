### String
- immutable (불변)하는 성질을 가진다.
```
String name = “hong”; //리터럴로 생성
String s1 = “hong”l
String s2 = “hong”;
```
- 라고 했을 때 s1과 s2는 위의 name이 생성한 “hong”을 가리킨다.
- 리터럴로 생성하면 String Pool이라는 공간에 생성이 되는데 이 메모리 공간에 있는 문자열 값은 변하지 않는다.
- 그래서 + 연산이나 .concat() 연산을 수행하면 문자열이 변하는 것이 아니라 새로운 문자열을 String Pool 안에 생성한다.
- 가비지 컬렉션을 해야하고 오버헤드가 발생하여 성능이 떨어진다.
- 하지만 불변한다는 특징 때문에 read연산시에는 StringBuffer와 StringBulider에 비해 빠르다는 장점과 멀티 쓰레드 환경에서 동기화에 유리하다는 장점이 있다.

### StringBuffer
- mutable 하는 성질을 가진다.
- 문자열을 new로 한 번만 만들고 메모리의 값을 변경시켜 문자열을 변경할 수 있다.
- 문자열 연산이 자주 있을 때 사용하는 것이 좋다.
- 멀티 쓰레드 환경에서 synchronized 키워드가 있어 동기화가 가능하다.

### StringBuilder
- StringBuffer와 같은 기능을 가지지만 synchronized 키워드가 존재하지 않는다.
- 동기화를 고려하지 않기 때문에 싱글 쓰레드 환경에서 StringBuffer보다 나은 성능을 보여준다.


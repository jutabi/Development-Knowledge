#싱글톤 패턴 (Singleton pattern)

애플리케이션이 시작될 때 어떤 클래스가 최초 한 번만 메모리를 할당하고 그 메모리에 인스턴스를 만들어 사용하는 디자인패턴
생성자가 여러 차례 호출되더라도 실제 생성되는 객체는 하나.
인스턴스가 필요하다면 기존의 인스턴스를 사용하도록 한다.

##싱글톤 클래스, 인스턴스 생성 방법

###1. Thread safe Lazy initialization (게으른 초기화)

```
public class ThreadSafeLazyInitialization {
    // 인스턴스 변수 생성
    private static ThreadSafeLazyInitialization instance;
    // private으로 외부에서 생성 금지
    private ThreadSafeLazyInitialization(){}
    // synchronized를 통해 thread-safe (큰 성능저하 발생)
    public static synchronized ThreadSafeLazyInitialization getInstance(){
        if (instance == null) {
            instance = new ThreadSafeLazyInitialization();
        }
        return instance;
    }
}
```

###2. Thread safe lazy initialization + Double-checked locking
```
public class ThreadSafeLazyInitialization {
    private volatile static ThreadSafeLazyInitialization instance;
    private ThreadSafeLazyInitialization() {}
    public static ThreadSafeLazyInitialization getInstance(){
        // 함수에 synchronized를 사용하는 것이 아니라 인스턴스 여부를 체크하고
        if (instance == null){
            synchronized (ThreadSafeLazyInitialization.class) {
                // 두 번째 if문에서 다시 한번 체크할 때 동기화 시켜서 인스턴스 생성
                if (instance == null)
                    instance = new ThreadSafeLazyInitialization();
            }
        }
        return instance;
    }
}
```

###3. Initialization on demand holder idiom (holder에 의한 초기화)
```
public class Something {
    private Something() {
    }
    private static class LazyHolder {
        public static final Something INSTANCE = new Something();
    }
    public static Something getInstance() {
        return LazyHolder.INSTANCE;
    }
}
```
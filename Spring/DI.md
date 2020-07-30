# DI (Dependency Injection, 의존성 주입)
### 의존성
- B 클래스에서 A 클래스를 사용한다고 할 때 B 클래스는 A 클래스에 의존 관계를 가진다.
```
class A {
    ...
}
class B {
    private A a;
    public void method() {
        ...
        this.a = new A();
        sout(a.name);
    }
}
```  
- A 클래스와 B 클래스간의 결합도가 높아진다.
- A 클래스의 내용을 변경하면 B 클래스도 그에 따른 영향이 생긴다.
- 단위테스트를 하기 어려워진다.

### 주입
- B 클래스를 사용할 때 다른 객체를 인자로 전달하는 것을 주입이라 한다.
```
class B {
    public B(A a) {
        ...
    }
}
```

### + [Dependency Inversion Principle (의존성 역전 원리)](../Design%20Pattern/SOLID/Dependency_inversion_principle.md)

### 의존성 주입
- B 클래스가 동작하는데 A 클래스가 필요할 때 ***B 클래스 내에서 A 객체를 생성하는 것이 아닌***
A 객체를 B 클래스에 전달하고 그것을 이용하여 B 클래스가 동작하는 것을 말한다.
- 스프링 프레임워크에서는 A 클래스를 스프링 컨테이너 안에  Bean 이라는 것으로 등록을 하고 
B 클래스를 사용 할 때 ***스프링 컨테이너에서 A 클래스 Bean 을 주입***해주어 사용한다.
    #### 스프링 프레임워크에서의 의존성 주입
    - MemberService.java
    ```
  @Service
  public class MemberService implements IMemeberService {
    ...
  }
  ```
    - MemberController.java
  ```
  @Controller
  @RequestMapping(...)
  public class MemberController {
    private final MemberService service;
  
    @Autowired
    public MemberController(MemberService memberService) {
        this.service = memberService;
    }
  }
  ```
  위의 코드와 같이 MemberController 클래스가 동작하기 위해 MemberService 클래스가 필요하다고 할 떄  
  MemberController 내에서 
  ```
  MemberService service = new MemberService();
  ```
  와 같이 객체를 생성하는 것이 아니라  
  ```
  public MemberController(MemberService memberService)
  ```
  위와 같이 bean 으로 등록되어 있는 memberService 객체를 주입하여 사용하는 것을 ***의존성 주입***이라고 한다.
  
    > 위의 방법은 @Service, @Autowired 어노테이션을 이용한 의존성 주입 방법이다.  
    아래와 같이 applicationContext.xml에 bean을 등록하여 사용하는 방법도 존재한다.
    ```
    <bean id="memberService" class="ems.member.dao.MemberService" ></bean>
    
    <bean id="memberController" class="com.project.member.MemberController">
        <constructor-arg ref="memberService" ></constructor-arg>
    </bean>
    ```


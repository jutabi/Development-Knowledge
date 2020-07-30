# REST (Representational State Transfer)
- 자원을 이름으로 구분하여 해당 자원의 상태(정보)를 주고 받는 것
- 자원: 소프트웨어가 관리하는 모든 것
    - 문서, 그림, 데이터, 소프트웨어 자체
- 자원을 표현하기위해 이름을 쓴다
    - DB의 학생 정보가 자원이라면 ‘student’을 자원의 표현으로
- 상태 전달
    - 데이터가 요청되는 시점에서 자원의 상태(정보)를 전달
    - JSON 혹은 XML을 통해 데이터를 주고 받는 것이 일반적
- World Wide Web과 같은 분산 하이퍼미디어 시스템을 위한 소프트웨어 개발 아키텍처의 한 형식
- REST는 기본적으로 웹의 기존 기술과 HTTP프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처
- HTTP URI(Uniform Resource Identifier)(URL (x)(상위개념))를 통해 자원을 명시하고 HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용
     - POST: Create
     - GET: Read
     - PUT: Update
     - DELETE: Delete
     - HEAD: HEAD(header 정보 조회)
- 자원 기반의 구조, 설계의 중심에 자원이 있고 HTTP Method를 통해 자원을 처리하도록 설계된 아키텍처

## REST의 장점
- HTTP프로토콜의 인프라를 그대로 사용함으로 REST API사용을 위해 별도 인프라 구축 불필요
- HTTP프로토콜의 표준을 활용하여 HTTP의 장점을 가져 감
- HTTP표준 프로토콜에 따르는 모든 플랫폼에서 사용가능
- Hypermedia API의 기본을 충실히 하며 범용성도 보장
- REST API 메시지가 의도하는 바를 명확하게 나타냄
- 여러가지 서비스 디자인에서 생길 수 있는 문제를 최소화
- 서버와 클라이언트의 역할을 명확하게 분리

## REST의 단점
- 표준이 존재하지 않는다
- 사용 가능한 CRUD 4가지뿐이다
- 구형브라우저에서 PUT과 DELETE를 사용하지 못하고 pushState를 지원하지 않는다

## REST가 필요한 이유
- 어플리케이션 분리 및 통함
- 다양한 클라이언트의 등장
- 다양한 브라우저와 모바일기기에서도 통신 가능하여야 함

## REST의 구성 요소
#### 1. 자원(Resource): URI
- 모든 자원에는 고유한 ID가 존재하며 Server에 있다
- ID는‘/students/:student_id’와 같은 HTTP URI
- 클라이언트는 URI를 이용하여 자원을 지정하고 자원의 상태(정보)에 대한 조작을 Server에 요청

#### 2. 행위(Verb): HTTP Method
- POST: Create
- GET: Read
- PUT: Update
- DELETE: Delete

#### 3. 표현(Representation of Resource)
- 클라이언트가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답(Representation)
    을 보낸다
- REST에서 하나의 자원은 JSON, XML, TEXT, RSS등 여러 형태의 Representation으로
    나타내어 질 수 있다.
- JSON혹은 XML을 통해 데이터를 주고받는 것이 일반적

## REST의 특징
#### 1. Server - Client구조
- 자원이 있는 서버와 요청하는 클라이언트의 구조이다.
    - REST Server: API를 제공하고 로직 처리 및 저장을 책임
    - Client: 사용자 인증이나 context(세션, 쿠키)등을 직접 관리하고 책임진다.
- 서로의 의존성이 줄어든다.

#### 2. Stateless(무상태)
- HTTP프로토콜이 Stateless임으로 REST역시 Stateless이다.
- Client의 context를 Server에 저장하지 않는다.
- Server는 각각의 요청을 별개의 것으로 인식하고 처리한다.
    - 각 API서버는 Client의 요청만을 단순 처리한다.
    - 이전 요청이 다음 요청의 처리에 연관되지 않는다.
    - 이전 요청이 DB를 수정하여 DB에 의해 바뀌는 것은 허용
    - Server의 처리 방식에 일관성을 부여하고 부담이 줄어들며, 서비스의 자유도가 높아진다.

#### 3. Cacheable(캐시 처리 가능)
- 웹 표준 HTTP프로토콜을 사용하기에 캐시 처리 기능 적용가능
    - Last_Modified태그나 E-Tag를 이용하면 구현이 가능
- 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구됨.
- 응답시간이 빨라지고 서버의 트랜잭션이 발생하지 않아 전체응답시간, 성능, 서버의 자원 이용률이 향상된다.

#### 4. Layered System(계층화)
- Client는 REST API Server만 호출한다.
- REST Server는 다중 계층으로 구성 가능하다.
- 프록시, 게이트웨이 같은 네트워크 기반의 중간매체 사용 가능

#### 5. Code-On-Demand (Optional)
- Server로부터 스크립트를 받아서 Client에서 실행한다.

#### 6. Uniform Interface(인터페이스의 일관성)
- URI로 지정한 자원에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다.
- HTTP표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하고 특정 언어나 기술에 종속되지 않는다.

## REST API
- REST기반으로 서비스 API를 구축한 것을 말한다.
- 최근 OpenAPI, 마이크로서비스 등을 제공하는 업체 대부분은 REST API를 제공한다.
- 사내 시스템들도 REST기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을
    편하게 함.
- HTTP표준을 기반으로 구현하므로, HTTP를 지원하는 프로그래밍 언어로 클라이언트와 서버 구현 가능.
    - REST API를 제작하면 델파이, 자바, C#, 웹 등을 통해 클라이언트 제작이 가능하다는 것

### 리소스 원형
- 도큐먼트: 객체 인스턴스나 데이터베이스 레코드와 유사
- 컬렉션: 서버에서 관리하는 디렉터리라는 리소스
- 스토어: 클라이언트에서 관리하는 리소스 저장소

## REST API 설계 기본 규칙
- URI는 정보의 자원을 표현해야 함
    - 리소스는 동사보다는 명사, 대문자보다는 소문자
    - 도큐먼트 이름으로는 단수명사
    - 컬렉션 이름으로는 복수명사
    - 스토어 이름으로는 복수명사
- 자원에 대한 행위는 HTTP Method(CRUD)로 표현
    - URI에 HTTP Method가 들어가면 안된다.
        - GET /members/delete/1 -> DELETE /members/1
    - URI에 행위에 대한 동사 표현이 들어가면 안된다.
        - GET /members/show/1 -> GET /members/1
        - GET /members/insert/2 -> POST /members/2
    - 슬래시는 계층관계를 나타낸다.
        - http://example.com/houses/apartments
    - URI마지막 문자에는 슬래시를 포함하지 않는다.
    - 하이픈(-)을 사용하여 URI의 가독성을 높인다.
    - 밑줄(_)은 사용하지 않는다.
    - URI의 경로는 소문자를 사용하도록 한다.
         - RFC 3986(URI의 문법형식)은 URI 스키마와 호스트를 제외하고 대소문자를 구별하도록
         규정하고 있기 때문
    - 파일 확장자는 URI에 포함하지 않는다
    - 리소스 간에 연관 관계가 있는 경우에는
         - /리소스명/리소스ID/관계가 있는 다른 리소스명
         - GET: /users/{userid}/devices


## RESTful
- REST API를 제공하는 웹서비스를 RESTful하다라고 한다.
- REST의 원리를 따르는 시스템은 RESTful이란 용어로 지칭된다.
- CRUD기능을 모두 POST로 처리, route에 리소스, id외의 정보가 들어가는 경우 RESTful 하지
못하다고 한다.
- REST의 근본적인 목적이 성능향상보다는 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는
것이 주 동기이다.
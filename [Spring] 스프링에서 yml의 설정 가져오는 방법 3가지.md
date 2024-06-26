## **스프링에서 yml의 설정 가져오는 방법 3가지**

### 1.**@Value**
    
개별 속성 값을 나눠 주입     
타입 변환 자동 처리    
SpEL(Spring Expression Language)을 지원    
    - 프로퍼티 파일에서 값 주입: **`@Value("${property.key}")`**    
    - 기본 값 설정: **`@Value("${property.key:default_value}")`**    
    - 수학 연산 수행: **`@Value("#{19 + 1}")`**    
    - 메소드 호출 결과 주입: **`@Value("#{someBean.someMethod()}")`**    

Spring 3.0 ↑    
    
- 설정 값이 간단하거나, 복잡한 계산이 필요한 경우 SpEL과 함께 사용
    
    ```java
    @Component
    public class GoogleOAuthProperties {
    
        @Value("${google.oauth.clientId}")
        private String clientId;
    
        @Value("${google.oauth.clientSecret}")
        private String clientSecret;
    
        @Value("${google.oauth.redirectUri}")
        private String redirectUri;
    ```
<br>


    
### 2.**@ConfigurationProperties**
    
관련 속성들을 한 번에 바인딩     
관련된 속성들을 하나의 클래스로 그룹화하여 관리     
타입 안전성 제공(컴파일 타임에 프로퍼티 타입 체크)    
@Validated 어노테이션과 함께 사용하여 검증 로직을 추가 가능     
IDE 지원이 우수하여, 프로퍼티의 자동 완성, 탐색, 리팩토링 등이 가능    
    
**`@EnableConfigurationProperties`** 어노테이션을 사용하여 구성 클래스를 활성화해야 사용 가능     
**`@SpringBootApplication`** 있는 클래스에 이를 추가    
`@EnableConfigurationProperties`은 `@ConfigurationProperties`가 붙은 클래스를 스프링 컨텍스트에 빈으로 등록하기 위해 사용    
    ※ Spring Boot 2.2 버전 이상부터는 `@ConfigurationProperties`가 붙은 클래스를 자동으로 빈으로 등록    
Spring Boot 1.2.0 ↑ (Spring Boot의 일부)    
Spring 지원X    
    
- 여러 관련 설정을 하나의 빈으로 묶어 관리해야 할 때 유용
- 타입 안전성이 중요하거나, 설정 값에 대한 검증 로직을 추가해야 할 경우 유용
    
    ```java
    @Configuration
    @ConfigurationProperties(prefix = "google.oauth")
    public class *GoogleOAuthConfig {
    
        private String clientId;
        private String clientSecret;
        private String redirectUri;
    
        // Getters and setters
        public String getClientId() {
            return clientId;
        }
    ```
    
    ```java
    @SpringBootApplication
    @EnableConfigurationProperties(GoogleOAuthConfig.class)
    public class Application {
        // ...
    }
    ```
<br>



### 3.**Environment 인터페이스**
직접 속성 값을 조회    
애플리케이션의 현재 환경에 대한 정보 제공    
프로파일(**`profile`**)이나 프로퍼티(**`property`**) 접근에 사용됨    
프로그래밍 방식으로 속성값 조회 가능    
Spring 3.1 ↑     
    
- 실행 시점에 동적으로 프로퍼티 값을 결정해야 할 때 유용
- 여러 소스에서 프로퍼티 값을 읽어야 하거나, 프로퍼티 값에 따라 다른 로직을 실행해야 하는 경우
    
    ```java
    @Component
    public class GoogleOAuthPropertiesUsingEnv {
    
        private final Environment env;
    
        @Autowired
        public GoogleOAuthPropertiesUsingEnv(Environment env) {
            this.env = env;
        }
    
        public String getClientId() {
            return env.getProperty("google.oauth.clientId");
        }
    
        public String getClientSecret() {
            return env.getProperty("google.oauth.clientSecret");
        }
    
        public String getRedirectUri() {
            return env.getProperty("google.oauth.redirectUri");
        }
    }
    ```


## 간단 결론
- 간단한 값 주입이나, 동적 값 처리가 필요할 때 : **`@Value`**    
- 관련된 설정 값을 그룹화하거나, 타입 안전성이 중요할 때 : **`@ConfigurationProperties`**    
- 프로그래밍 방식으로 환경 및 프로퍼티 정보에 접근해야 할 때 : **`Environment`** 인터페이스   

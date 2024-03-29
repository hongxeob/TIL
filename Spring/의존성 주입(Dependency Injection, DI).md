# 스프링 DI

## 스프링에서 의존성 주입(Dependency Injection, DI)이란?

- Spring 프레임 워크 핵심 프로그래밍 모델 중 하나이다
- 외부에서 두 객체 간의 관계를 결정해주는 디자인 패턴
    - 인터페이스를 사이에 둬서 클래스 레벨에서는 의존관계가 고정되지 않도록 하고 런타임 시에 관계를 동적으로 주입해주는 것을 말한다
- 객체간 의존성을 개발자가 객채 내부에서 직접 호출(new 연산자)하는 대신, 외부(스프링 컨테이너)에서 객체를 생성해서 넣어주는 방식이다
- `애플리케이션 실행 시점(런타임)에 외부에서 실제 구현 객체를 생성하고 클라이언트에 전달해서 클라이언트와 서버의 실제 의존관계가 연결 되는 것을 말한다.`

## 의존성 주입을 해야 하는 이유

- `의존관계 주입을 사용하면 클라이언트 코드를 바꾸지 않고, 클라이언트가 호출하는 대상의 타입 인스턴스를 변경할 수 있다.`
- `의존관계 주입을 사용하면 정적(import문)인 클래스 의존관계를 변경하지 않고, 동적인 객체 인스턴스 의존관계를 쉽게 변경할 수 있다.`
- 테스트가 용이해진다
- 코드 재사용율이 높아진다
- 객체 간의 의존성을 줄이거나 없앨 수 있다
- 객체 간의 별합도를 낮추면서 유연한 코드를 작성할 수 있다

## 의존성 주입의 3가지 방법

### 1. 생성자 주입 (Constructor Injection) 

```java
@Controller
public class Di1Controller {
  //final을 붙일 수 있음
    private final Di1Service di1Service;
  //---------------------------------------------------------
  //@Autowired 
    public Di1Controller(Di1Service di1Service) {
        this.di1Service = di1Service;
    }
}
```

- 생성자를 통해서 의존관계를 주입 받는 방법이다
- 생성자에 `@Autowired`를 붙여 의존성을 주입받을 수 있다
    - 클래스의 생성자가 하나이고, 그 생성자로 주입받을 객체가 빈으로 등록되어 있다면 `@Autowired`를 생략 할 수 있다.
- 스프링 컨테이너가 올라오고 애플리케이션이 세팅되는 시점에 **생성자 주입을 통해 한번만 호출되는 것이 보장**된다
    - final을 사용할 수 있다 → **‘불변,필수’ 의존관계에서 사용된다**
- 대부분의 의존관계 주입은 한번 설정이 되고 나면 의존관계를 변경할 일이 없다

### 2. 필드 주입 (Field Injection)

```java
@Controller
public class Di2Controller {
	
    @Autowired 
    private Di2Service di2Service;
}
```

- 필드에 바로 주입을 하는 방식이다 (필드에 `@Autowired` 어노테이션을 붙여주면 자동으로 의존성 주입이 된다)
- 사용법이 간단해서 많이 접할 수 있는 방법이다
- 단점 :
    - 외부에서 **변경이 불가능**하기 때문에 테스트하기 힘들다
    - 코드가 간결하지만 외부에서 **변경하려면 setter**를 만들어야 한다
    - 생성자 주입과 다르게 final을 선언할 수 없어서, **객체가 변할 수 있다**

### 3. 수정자 주입(Setter Injection)

```java
@Controller
public class Di3Controller {
    private Di3Service di3Service;
    
    @Autowired
    public void setDi3Service(Di3Service di3Service) {
    	this.di3Service = di3Service;
    }
}
```

- Setter 메소드에 `@Autowired` 어노테이션을 붙이는 방법
- 선택적인 의존성을 사용할 때 유용하다
- 단점
    - 주입이 필요한 객체가 주입이 되지 않아도 얼마든지 객체를 생성할 수 있다는 것이 문제다
    - 수정자 주입을 사용하면 setXXX 메서드를 public으로 열어두어야 하기 때문에 **언제 어디서든 변경이 가능**하다

## 권장되는 주입 방식

>Spring Framwork reference에서 권장하는 방법은 **생성자를 통한 주입**이다

### 생성자 주입을 권장하는 이유

필수적으로 사용해야하는 의존성 없이는 Instance를 만들지 못하도록 강제할 수 있기 때문이다

- **순환 참조를 방지할 수 있다**
    - 의존 관계에 내용을 외부로 노출 시킴으로써 컴파일 시점에 오류를 체크할 수 있다
- **불변성을 유지한다**
    - 생성자로 의존성을 주입할 때 final로 선언할 수 있고, 이로 인해 런타임에서 의존성을 주입받는 객체가 변할 일이 없어진다
    - 그래서 누군가가 Controller 내부에서 Service 객체를 바꿔치기 할 수 없다
- **테스트에 용이하다**
    - DI의 핵심은 관리되는 클래스가 DI 컨테이너에 의존성이 없어야 한다
    - 메인 코드가 필드 주입으로 작성된 경우, 순수 자바 코드로 단위 테스트를 실행하는 것은 불가능하다
        - 메인 코드는 Spring 같은 DI 프레임워크 위에서 동작하지만, 테스트 코드는 그렇지 않아서 의존관계 주입이 null상태여서 NullPointError이 발생한다
    - 즉 독립적으로 인스턴스화가 가능한 POJO(Plain Old Java Object)여야 한다는 것이다

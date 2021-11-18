## DI (Dependency Injection, 의존성 주입)

### 의존성 주입이란?

- 의존성 주입은 의존하는 객체를 직접 생성하는 대신 의존 객체를 전달받는 방식을 말한다.

### 왜 의존성 주입을 사용해야 할까?

- 객체 간의 의존성과 결합도를 낮춰 유연한 코드를 작성할 수 있다.
- 코드의 재활용성을 높여준다.
- 유닛 테스트 작성을 용이하게 한다.
- 즉 의존성 주입을 사용하면 **유지보수가 쉬워지는 장점**이 있다.

### 예시

```java
public class Book {

}
```

```java
public class Student {
    private Book book;

    public Student() {
        this.book = new book();
    }
}
```

- 위 코드는 Student가 하는 행동을 나타낸 클래스이다.
- 만약 학생이 Book을 읽는 것 이외의 행동을 하려 한다면, **Student 클래스의 생성자 코드를 수정해야 한다.**
- 또한 올바른 OOP 설계를 했다면 객체들 간에 관계가 맺어져야한다. 하지만 위 코드는 **Book 클래스와 Student 클래스가 직접 관계를 맺고 있다.**
- 즉 위의 두 클래스는 서로 강하게 결합되어 있으며, 이로 인해 유연성이 떨어진다고 볼 수 있다.

### 의존성 주입 적용

```java
public interface Action {

}
```

```java
public class Book implements Action {

}
```

```java
public class Game implements Action {

}
```

```java
public class Student {

    private Action action;

    // 1. 생성자 주입
    @Autowired
    public Student(Action action) {
        this.action = new action();
    }

    // 2. 설정자 주입
    @Autowired
    public void setAction(Action action) {
        this.action = action;
    }
}
```

```java
public class Student {
    // 3. 필드 주입
    @Autowired
    private Action action;
}
```

- 의존성 주입 방식을 사용하여 Student는 Action에만 집중할 수 있게 되었다. 
- Action은 인터페이스이기 때문에 어떤 Action을 할 것인지는 Student 클래스 외부에서 결정된다.
- Student가 지금 하고 있는 Action이 아닌 다른 Action을 하게 되어도, Student 클래스의 코드를 수정하지 않아도 된다.
- 즉 의존성 주입을 통해 관련된 클래스 간의 결합도를 낮추고, 유연성을 높였다고 할 수 있다.

### 의존성 주입의 세가지 방법
1. 생성자 주입 (Construction Injection)

    - **생성자 주입은 스프링에서 가장 권장하는 의존성 주입 방법이다.**
    - 필수적으로 사용해야 하는 참조 객체 없이는 인스턴스를 만들지 못하게 강제한다.
    - **즉 의존성이 주입되지 않아 발생할 수 있는 NullPointerException을 방지할 수 있다.**
    - 순환 참조 의존성을 애플리케이션을 실행하는 시점에서 체크할 수 있다.
    - 의존성 주입 대상 필드를 fianl로 불변 객체 선언할 수 있다.


2. 설정자 주입 (Setter Injection)

    - 의존성이 선택적으로 필요한 경우 사용한다.
    - 의존성 주입 대상 필드를 final로 선언 할 수 없다.


3. 필드 주입 (Field Injection)

   - **장점보다 단점이 많아 사용하지 않는 것을 권장한다.**
   - 가장 간단히 선언할 수 있다
   - 단위 테스트시 의존성 주입이 용이하지 않다.
   - 의존성 주입 대상 필드를 final로 선언 할 수 없다.
   
---
### 출처
- https://jgrammer.tistory.com/72
- https://mangkyu.tistory.com/125
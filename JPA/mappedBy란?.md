# mappedBy 란?

## 객체와 테이블간에 연관관계를 맺는 차이를 이해 해야함
1. 객체는 연관관계가 2개이다
    - 멤버->팀의 단방향 1개 + 팀->멤버의 단방향 1개
    - 즉 서로 다른 단방향 관계 2개
    - 객체를 양방향으로 참조혀려면 단방향 연관관계를 2개 만들어야 한다
2. 테이블에서는 연관관계가 1개
    - 팀 <->멤버의 양방향 1개 (FK키 하나로 양쪽 다 가능)

## 연관관계의 주인(Owner)

### 규칙

- 객체의 두 관계중 하나를 연관관계의 주인으로 지정
- **연관관계의 주인만이 외래키를 관리(등록,수정)**
- **주인이 아닌쪽은 읽기만 가능**
- 주인은 mappedBy 속성 사용X
- 주인이 아니면 mappedBy 속성으로 주인 지정

## 양방향 연관관계의 주의

- 순수 객체 상태를 고려해서 항상 양쪽에 값을 설정하다
- 연관관계 **편의 메소드**를 생성하자
    - ex) setter를 이름을 바꿔서? -> 정확하게 알수있게,그냥 단순 set 메서드가 아닌 의미를 알 수 있게!
        
        ```java
      // (member 클래스라면)
       public void changeTeam(Team team){
        
        this.team=team;
        
        team.getMembers().add(this);
      }
        ```
- 결국 주인과 주인이 아닌쪽 중 하나를 정해 그 메서드 안에서 주인과,주인이 아닌 값을 둘다 넣어준다
- 양방항 매핑시에 무한 루프를 조심하자
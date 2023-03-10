> 과거에는 데이터를 관리하기 위해 '파일 시스템'이라는 소프트웨어를 사용했다

# 문제점 !

-   같은 내용의 데이터가 중복 저장 된다.
-   응용 프로그램ㅇ이 데이터 파일에 종속적이다  
    \- 파일의 어떠한 부분을 변경,추가 하려면 관련된 모든 응용프로그램에서 파일에 접근하는 방법을 변경해야한다
-   데이터 파일에 대한 동시 공유,보안,회복 기능이 부족하다
-   응용 프로그램을 개발하기 쉽지 않다

> ## 그래서 등장한 데이터베이스 관리 시스템!!
> 
> 데이터베이스 시스템이란 데이터베이스에 데이터를 저장하고 이를 관리하여 조직에 필요한 정보를 제공해주는 시스템이다.

-   응용 프로그램을 대신하여 데이터베이스에 들어 있는 데이터를 삽입,삭제,수정,검색하고 모든 응용 프로그램이 데이터베이스를 공유 할 수 있게 한다

## 데이터베이스 관리 시스템의 주요 기능

-   정의 기능 : 데이터베이스 구조를 정의하거나 수정할 수 있다
-   조작 기능 : 데이터를 삽입,삭제,수정,검색하는 연산을 할 수 있다
-   제어 기능 : 데이터를 항상 정확하고 안전하게 유지할 수 있다

## 데이터베이스 관리 시스템의 장점

-   데이터 중복을 통제할 수 있다
-   데이터 독립성이 확보된다
-   데이터를 동시 공유할 수 있다
-   데이터 보안이 향상된다
-   데이터 무결성을 유지할 수 있다
-   표준화할 수 있다
-   장애 발생 시 회복이 가능하다
-   응용 프로그램 개발 비용이 줄어든다

## 데이터베이스 관리 시스템의 단점

-   비용이 많이 든다
-   백업과 회복 방법이 복잡하다
-   중앙 집중 관리로 인한 취약점이 존재한다

---

## 데이터베이스 관리 시스템의 발전 과정

### 1세대 : 네트워크 DBMS ,계층 DBMS

-   네트워크 DBMS : 데이터베이스를 그래프 형태로 구성  
    \- ex) IDS
-   계층 DBMS : 데이터베이스를 트리 형태로 구성  
    \- ex) IMS

### 2세대 : 관계 DBMS

-   관게 DBMS : 데이터베이스를 테이블 형태로 구성  
    \- 데이터베이스를 단순하고 이해하기 쉬운 구조로 구성한다는 장점이 있다.  
    \- ex) 오라클 ,MySQL,마리아DB

### 3세대 : 객체지향 DBMS, 객체관계 DBMS

-   객체지향 DBMS : 객체를 이용해 데이터베이스를 구성  
    \- 오투,온투스,젬스톤(GemStone)
-   객체관계 DBMS : 객체 DBMS + 관게 DBMS

### 4세대 이후 : NoSQL,NewSQL DBMS

-   수많은 사람들이 소셜 네트워크 서비스를 폭발적으로 이용하면서 사진,동영상,검색로그와 같은 비정형 데이터가 대량으로 쏟아지며 등장
-   데이터 구조를 미리 정해두지 않기 때문에 비정형 데이터를 저장하고 처리하는데 적합
-   확장성이 뛰어남
-   예시로는 몽고DB,카산드라,레디스 등이 있다.
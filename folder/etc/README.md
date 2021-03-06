# ETC
## 면접 대비용으로 간단 정리
- [참조 1](https://github.com/ksundong/backend-interview-question)
- [참조 2](https://github.com/JaeYeopHan/Interview_Question_for_Beginner)

### Java
1. [jvm](./folder/jvm.md) 
2. classloader
3. [GC](./folder/GC.md)
4. [Java Collection](./folder/Java_Collection.md)
5. Vector vs ArrayList 
   1. Vector : thread-safe
   2. ArrayList : Not Thread-safe
6. HashSet vs TreeSet vs LinkedHashSet
   1. HashSet : 순서 보장 안됨. 중복 안됨
   2. TreeSet : 정렬된 상태. 중복 안됨
   3. LinkedHashSet : 저장 순서 유지 HashSet
7. HashMap vs HashTable vs TreeMap vs LinkedHashMap vs ConcurrentHashMap
   1. HashMap : null 가능
   2. HashTable : thread-safe, null x
   3. TreeMap : key 값 기준 정렬된 상태
   4. LinkedHashMap : 입력된 순서 상태
   5. ConcurrentHashMap : thread-safe, read는 동기처리 안함(성능 향상), null x
8. Java Stream
9. collection vs Stream
   1. collection : 자료 구조에 가깝다
   2. stream : 데이터 처리에 가깝다
10. Java 동기화 방법
11. '==' vs equal vs hashcode
12. String, StringBuilder, StringBuffer
    1.  String: 
        1. "ab" = new String("ab") : false
        2. "ab".equal(new String("ab")) : true
        3. "ab" 
           1. 위치 : heap의 String constant pool
           2. 동일문자는 같은 레퍼런스 주소 공유
        4. new String("ab") : 일반 객체처럼 그냥 heap  
    2.  StringBuilder
        1.  not thread-safe
        2.  memory에 append 방식
    3.  StringBuffer 
        1.  thread-safe
        2.  memory에 append 방식
13. reflection
14. generic
15. jdk vs jre
16. [HashMap key object](https://www.baeldung.com/java-custom-class-map-key)
    1.  key로 객체를 사용시 hashcode와 equal 재정의 필요. 왜?
    2.  그리고 객체는 immutable 해야됨. 왜? 


### DB (Mysql 기준)
1. DB Transaction
   1. 논리적 처리 단위
   
   2. ACID
      1. 원자성(Atomicity) - `all or nothing`
         1. 트랜잭션 내에서 모두 성공하거나 혹은 모두 실패해야 합니다.
      
      2. 일관성(Consistency) - 제약 조건에 따라 관리되는 상태
         1. 모든 트랜잭션은 일관성있는 데이터베이스 상태를 유지해야 합니다. 
         2. 예를 들면 데이터베이스에서 정한 `무결성 제약 조건`을 항상 만족해야 합니다.
      
      3. 격리성(Isolation)
         1. 동시에 실행되는 트랜잭션들이 서로에게 영향을 미치지 않도록 격리해야 합니다. 
         2. 예를 들면 동시에 같은 데이터를 수정하지 못하도록 해야 합니다. 
         3. 격리성은 `동시성`과 관련된 성능 이슈로 인해 `격리 수준`을 선택할 수 있습니다.
      
      4. 지속성(Durability) - 기록
         1. 트랜잭션을 성공적으로 끝내면 그 결과가 항상 기록되어야 합니다. 
         2. 중간에 시스템에 문제가 발생하더라도 데이터베이스 로그 등을 사용해서 성공한 트랜잭션 내용을 복구해야 합니다.
   
   3. 격리 수준 isolation Level
      1. 특정 트랜잭션이 다른 트랜잭션에서 변경하거나 조회하는 데이터를 볼 수 있도록 허용할지 말지를 결정
      2. 종류
         1. READ UNCOMMITTED
         2. READ COMMITTED
         3. REPEATABLE READ : mysql default
         4. SERIALIZABLE

2. DB Index
   1. 탐색 효율 올리고 생성/수정/삭제 성능 떨어짐
   2. B+Tree
   3. Hashing 

3. mysql storage engine 별 특징
   
   1. innodb
      1. row lock
      2. MVCC (Multi Versioning Concurrency Control)
         1. 잠금을 사용하지 않는 일관된 읽기를 제공. 언두 로그를 이용한 기능 구현
         2. UPDATE 쿼리가 실행되면 InnoDB 버퍼 풀은 즉시 새로운 데이터로 변경되며 기존의 데이터는 언두(Undo)로 복사
      3. 트랜잭션, fk 가능
      4. 데이터와 index가 같은 파일로 관리
      
      5. 언두 영역
         1. UPDATE 문장이나 DELETE 문장으로 데이터를 변경했을 때 변경되기 전의 데이터(이전 데이터)를 보관
         2. 용도
            1. 트랜잭션의 롤백 대비용
            2. 트랜잭션의 격리 수준을 유지하면서 높은 동시성을 제공
      
      6. `인서트 버퍼` : 레코드가 INSERT 되거나 UPDATE 될 때는 데이터 파일을 변경하는 작업 뿐 아니라 해당 테이블에 포함된 인덱스를 업데이트하는 작업도 필요합니다. 그런데 `인덱스를 업데이트하는 작업`은 `랜덤하게 디스크를 읽는 작업`이 필요하므로 테이블에 인덱스가 많다면 이 작업은 상당히 많은 자원을 소모하게 됩니다. 그래서 `InnoDB는 변경해야 할 인덱스 페이지`가 `버퍼 풀에 있으면 바로 업데이트를 수행`하지만, 그렇지 않고 `디스크로부터 읽어와서 업데이트해야 한다면 이를 즉시 실행하지 않고 임시 공간에 저장해 두고 바로 사용자에게 결과를 반환`하는 형태로 성능을 향상시키게 되는데, 이 때 사용하는 임시 메모리 공간을 인서트 버퍼(Insert Buffer) 라고 합니다.
      
      7. `리두(Redo) 로그 및 로그 버퍼` : 쿼리 문장으로 데이터를 변경하고 커밋하면 DBMS는 데이터의 ACID를 보장하기 위해 즉시 `변경된 데이터의 내용을 데이터 파일로 기록`해야 합니다. 하지만 이러한 데이터 파일의 변경 작업은 순차적으로 많은 데이터를 한꺼번에 변경하는 것이 아니고 랜덤하게 디스크에 기록해야 하기 때문에 디스크를 상당히 바쁘게 만드는 작업입니다. 그래서 이러한 부하를 줄이기 위해서 대부분의 DBMS에는 변경된 데이터를 버퍼링해 두기 위해 InnoDB 버퍼 풀과 같은 장치가 포함되어 있습니다. 하지만 이 장치만으로 ACID를 보장할 수 없는데 이를 위해 `변경된 내용을 순차적으로 디스크에 기록하는 로그 파일`을 가지고 있습니다. 더 정확한 명칭은 리두 로그입니다.
      
      8. 테이블과 인덱스를 테이블 스페이스에 저장을 하고 테이블 스페이스는 몇개의 서버파일이나 디스크 파티션으로 구성
      
      9. 트랜잭션 처리가 필요하고 대용량의 데이터를 다루는 부분에서 효율적
      
      10. [Adaptive Hash Index](https://tech.kakao.com/2016/04/07/innodb-adaptive-hash-index/)
          1. 자주 사용되는 칼럼을 해시로 정의하여, B-Tree 를 타지 않고 바로 데이터에 접근할 수 있는 기능
      
      11. Clustered Index(클러스터형 인덱스)
          1. ![그림](https://hoing.io/storage/2020/11/Structure-of-Clustered-Index.jpg)
          
          2. InnoDB의 테이블은 Primary Key 값을 기반으로 구성되며 Cluster 라는 용어 의미대로 PK 값이 비슷한 레코드끼리 묶어서 저장되어 사용하고 그것을 Clustered Index(PK) 라고 합니다.
          
          3. PK 값으로 클러스터링된 테이블은 PK 값 자체에 대한 의존도가 높기 때문에 Clustered Index(PK) 의 열을 수정하는 것은 매우 많은 비용이 들어갑니다.
          
          4. Clustered Index 의 구조는 일반 B-Tree 인덱스와 비슷한 구조로 되어 있으나 B-Tree Index 와 달리 Clustered Inex의 리프노드에는 레코드의 모든 컬럼 값이 같이 저장되어 있습니다. Clustered Index 그 자체가 하나의 테이블이며 인덱스 구조로 관리 되는 것입니다.
 
   2. MyIsam
      1. 테이블 lock
      2. 데이티와 index가 다른 파일로 관리
      3. 트랜잭션 처리가 필요 없고, Read only 기능이 많은 서비스일수록 효율적
      4. 데이터 무결성에 대한 보장이 되지 않음

   3. memory
      1. 임시 테이블 사용시 사용
      2. 현재 최신 버전은 다른 스토리지 엔진 사용(이름 모르겠음)

4. MVCC(Multi Version Concurrency Control)

5. RDBMS vs NoSQL
   1. RDBMS
      1. 엄격한 데이터 관리 형태
      2. scale out 힘듬
      3. mysql, oracle, postgresql
   2. NoSQL
      1. 유연한 데이터 모델
      2. scale out 용이
      3. 데이터 일관성 관리가 상대적으로 힘듬
      4. redis, mongodb, 카산드라

### Spring

1. Intercepter vs Filter
   1. 공통점 : 요청 가로채서 공통 처리하기
   2. 차이점 : 
      1. Intercepter : spring context 안
      2. Filter : spring context 밖

2. AOP(Aspect-Oriented Programming)
   1. 공통 관심사를 모듈화할 수 있는 프로그래밍 기법
   2. Proxy 패턴 
   
   3. 핵심 기능에 공통 기능을 추가하는 3가지 방법
      1. 컴파일 : 자바 파일을 클래스 파일로 만들 때 바이트코드를 조작하여 적용된 바이트코드를 생성
      2. 로드 타임 : 컴파일은 원래 클래스 그대로 하고, 클래스를 로딩하는 시점에 끼워서 넣는다.
      3. `런타임`(스프링 방식) : A라는 클래스를 빈으로 만들 때 A라는 타입의 프록시 빈을 감싸서 만든 후에, 프록시 빈이 클래스 중간에 코드를 추가해서 넣는다.
   
   4. 용어 정리
      1. Aspect : 포인트컷과 어드바이스의 결합
      2. 위빙(Weaving) : 횡단 관심 메소드가 삽입되는 과정
      3. Advice : what
      4. Pointcut : 특정 조건에 의해 필터링된 조인포인트
      5. Join point : 후보 Pointcut 

3. Transaction 전파

4. JPA
   
   1. 관계주인 : fk 가진 엔티티가 연관관계 주인
      1. 보통 many 쪽이 fk를 가짐
   
   2. 영속성 컨텍스트 
      1. 엔티티 영구 저장 환경
      2. entitymanager를 통해 접근
      3. 구조
         1. 쓰기 지연 SQL 저장소
            1. 트랜잭션 종료시 flush() 호출하여 누적된 쿼리를 실 디비 반영
               1. entitymanager로 직접 호출 가능
         2. 1차 캐시
   
   3. 엔티티 변경
      1. 엔티티 변경 감지 : dirty checking
      2. merge 사용 : 준영속 상태를 영속 상태로 변경할 때 사용하는 기능
         1. 동작 방식
            1. 준영속 엔티티의 식별자 값으로 영속 엔티티를 조회한다.
               1. 영속 컨텍스트에 없으면 디비에서 가져옴???(추측 확인 필요)
            2. 영속 엔티티의 값을 준영속 엔티티의 값으로 모두 교체한다.(병합한다.)
            3. 트랜잭션 커밋 시점에 변경 감지 기능이 동작
   
   4. 엔티티 상태
      1. 비영속 : 영속성 컨텍스트와 전혀 관계가 없는 상태
      2. 영속 : 영속성 컨텍스트에 관리되는 상태
      3. 준영속 : 영속성 컨텍스트에 저장되었다가 분리된 상태
         1. 영속성 컨텍스트에서 더이상 관리하지 않을때(분리된)의 상태
         2. 영속성 컨텍스트가 제공하는 기능을 사용할 수 없습니다.
         3. 준영속 상태로 만드는 3가지 방법
            1. entityManager.detach(entity); // 해당 entity를 detach메서드를 통해 준영속 상태로 만든다.
            2. entityManager.clear(); // 영속성 켄텍스트를 초기화한다.
            3. entityManager.close(); // 영속성 컨텍스트를 종료한다.
   
   5. entity manager(not thread-safe)
      1. entitymanagerFactory(thread-safe)에 의해 request 당 생성
      2. 내부적으로 db connection 사용
      3. db 연결이 꼭 필요한 시점까지 커넥션을 얻지 않는다.
   
   6. 1차 캐시 vs 2차 캐시
      1. 1차 캐시 : 요청 응답 까지 유지(request 당 독립된 공간)
      2. [2차 캐시](https://www.youtube.com/watch?v=IJ3W6xEx8Oo) : 
         1. 어플리케이션 범위의 공유 캐시
         2. 동시성 보장을 위해 엔티티 원본 복사본 1차 캐시 전달
   
   7. [OSIV(Open Session In View)](https://ykh6242.tistory.com/102) : 기본값 true
      1. 영속성 컨텍스트 유지 범위
      2. 설정이 true 일때 작동방식 
         1. 클라이언트의 요청이 들어오면 서블릿 필터나, 스프링 인터셉터에서 영속성 컨텍스트를 생성한다. 단 이 시점에서 트랜잭션은 시작하지 않는다.
         2. 서비스 계층에서 @Transeactional로 트랜잭션을 시작할 때 1번에서 미리 생성해둔 영속성 컨텍스트를 찾아와서 트랜잭션을 시작한다.
         3. 서비스 계층이 끝나면 트랜잭션을 커밋하고 영속성 컨텍스트를 플러시한다. 이 시점에 트랜잭션은 끝내지만 영속성 컨텍스트는 종료되지 않는다.
         4. 컨트롤러와 뷰까지 영속성 컨텍스트가 유지되므로 조회한 엔티티는 영속 상태를 유지한다.
         5. 서블릿 필터나, 스프링 인터셉터로 요청이 돌아오면 영속성 컨텍스트를 종료한다. 이때 플러시를 호출하지 않고 바로 종료한다.
      3. 장/단점
         1. 장점 : 프레젠테이션 layer 에서 entity lazy 로딩 사용 가능
         2. 단점 : 커넥션을 영속성 컨텍스트가 종료될 때까지 1:1로 계속 물고 있음(실시간 처리에 병목발생 높음)
      4. 덧붙이기
         1. 영속성 컨텍스트는 기본적으로 트랜잭션 범위 안에서 엔티티를 조회/수정할 수 있다.
         2. 영속성 컨텍스트는 트랜잭션 범위 밖에서 엔티티를 조회만 할 수 있다. 
            1. 트랜잭션 없이 읽기(Nontransactional reads)
      5. 트랜잭션 범위 밖에서 영속성 컨텍스트의 변경 감지에 의한 데이터 수정이 다음 2가지 이유로 동작하지 않는다.
         1. 데이터베이스에 반영하려면 영속성 컨텍스트를 플러시(flush)해야 한다. 스프링이 제공하는 OSIV는 요청이 끝나면 플러시를 호출하지 않고 em.close()로 영속성 컨텍스트만 종료시켜 버린다.
         2. 강제로 플러시해도 트랜잭션 범위 밖이므로 데이터를 수정할 수 없다는 예외가 일어난다.
            1. 발생예외 : javax.persistence.TransactionRequiredException
   
   8. fetchtype eager vs lazy
   
   9. N+1 문제
      1. 연관 관계가 설정된 엔티티를 조회할 경우에 조회된 데이터 갯수(n) 만큼 연관관계의 조회 쿼리가 추가로 발생
      2. eager, lazy 둘 다 발생
         1. findByxxx, jpql 로 할 시 eager도 발생
         2. lazy는 연관 관계 객체가 프락시이므로 참조시점에 query 조회
      3. 해결법
         1. JPQL fetch join
            1. 패치 조인의 단점
               1. JPA가 제공하는 Pageable 기능 사용 불가
         2. @EntityGraph
         3. 공통적으로 카테시안 곱(Cartesian Product)이 발생
            1. 해결방안
               1. 일대다 필드의 타입을 Set으로 선언
               2. distinct를 사용하여 중복을 제거
   
   10. 매핑시 Fetch 전략을 Lazy로 설정해도 EAGER로 동작하는 경우가 있다.
   
      1. [참조](https://1-7171771.tistory.com/143)
      2. OneToOne 양방향
      3. 연관관계의 주인이 호출할 때는 지연 로딩이 정상적으로 동작하지만, 연관관계의 주인이 아닌 곳에서 호출한다면 지연 로딩이 아닌 즉시 로딩으로 동작한다
      
      4. 연관관계의 주인이 아닌 쪽에서 조회하게 되면 프록시 객체를 생성할 수 없기 때문에 지연 로딩으로 설정해도 즉시 로딩으로 동작하게 된다. 그 이유는 프록시는 null을 감쌀 수 없기 때문에 참조하고 있는 객체가 null인지 null이 아닌지 확인하는 쿼리를 실행해야 하기 때문이다.
      
      5. [OneToMany는 Lazy로딩 으로 동작하는 이유는?](https://woodcock.tistory.com/23)
         1. OneToMany에서는 Lazy로딩이 기본 설정이다. 일대다 관계에서는 일 측에서는 컬럼을 갖고있지 않는다. 그렇다면 일대일과 같이 값을 모르는데,  어떻게 Lazy로딩이 동작할 수 있을까? 이유는 아주 간단하다. 컬렉션은 값이 비어있다고 표현이 가능하지만(isEmpty), 1:1관계에서는 값이 없다면 null로 표현을 해야하기 때문이다. 즉 그렇기 때문에 컬렉션은 proxy로 가져올 수 있기 때문에 Lazy 로딩을 사용할 수 있다.
      
      6.  해결방안
         
         2. 구조 변경하기
            1. 양방향 매핑이 반드시 필요한 상황인지 다시한번 생각해본다.
            2. OneToOne -> OneToMany 또는 ManyToOne 관계로 변경이 가능한지 생각해본다.
         
         3. 구조를 유지한채 해결하기
            1. CART를 조회할때 USER도 함께 조회한다. (Fetch Join)
            2. batch fetch size를 사용한다.
   
   11. QueryBuilder : QueryDSL

5. JPA vs Mybatis
   1. JPA : 
      1. Java Persistence API의 약자로 Java ORM(Object-relational mapping) 기술에 대한 API 표준 명세
      2. 객체 관계 설정
      3. SQL 추상화 기술 : 데이터베이스에 종속적이지 않음
      4. 컴파일 타임에 오류를 확인 가능
      5. spec 일뿐 구현체는 따로 있음. ex) hibernate
   2. Mybatis 
      1. 퍼시스턴스 프레임워크(SQL Mapper)

6. security
   1. oauth2 client


### Network
1. TCP(Transmission Control Protocol, 전송제어 프로토콜) 
   
   1. 신뢰성 / 연결형 프로토콜
      1. 가상 회선
   
   2. 전이중(full-duplex), 점대점(point to point)방식 
      1. `전이중이란` 전송이 `양방향으로 동시에 일어날 수 있음`을 의미 
      2. 점대점이란 각 연결이 정확히 2 개의 종단점을 가지고 있음을 의미 
   
   3. 멀티캐스팅이나 브로드캐스팅을 지원하지 않는다.
   
   4. #### 연결 생성 3 way handshake
      ![tcp 3 way](https://t1.daumcdn.net/cfile/tistory/225A964D52F1BB6917) 
      
      1. active open
         - Closed -> SYN-SENT -> ESTABLISHED
      
      2. passive open
         - Closed -> LISTEN -> SYN-RECEIVED -> ESTABLISHED
   
   5. #### 연결 종료 4 way handshake
      ![tcp 4 way](https://t1.daumcdn.net/cfile/tistory/2152353F52F1C02835)
      
      1. active close(연결 종료 요청한쪽)
         - Established -> FIN_WAIT_1 -> FIN_WAIT_2 -> TIME_WAIT(2 * MSL(Maximum Segment Life)) -> CLOSED
      
      2. passive close(연결 종료 받음쪽)
         - Established -> CLOSE_WAIT -> LAST_ACK -> CLOED

2. UDP(User Datagram Protocol, 사용자 데이터그램 프로토콜)
   1. 비신뢰성 / 비연결형 
   2. 흐름제어, 오류제어 또는 손상된 세그먼트의 수신에 대한 재전송 (X) 
   3. ex. DNS

3. HTTPS
   1. 암호화된 HTTP
   2. 공개키로 대칭키를 전달
   3. 실 데이터 전달은 대칭키로 암호화
   4. 공개키 + 대칭키 혼합을 사용

4. brower와 서버 통신 과정
   1. 브라우저가 서버에 요청
      1. if 요청이 domain 일 경우 
         1. local dns 확인
         2. remove dns 확인
            1. ISP DNS
               1. 캐싱 되어 있다면 바로 응답 
               2. 캐싱 되어 없으면 
                  1. root dns -> domain zone dns 까지 탐색하여 결과를 캐싱하여 client에 응답
   2. client TCP/IP 계층 내려감
      1. TCP : 요청 데이터 분할 + port(client, server)
      2. IP : 패킷 + IP(client, server)
      3. 물리계층 : 신호 만듬
   3. client와 server 사이 네트워크
      1. LAN 
      2. 라우터 -> 라우터 (hop)
   4. server TCP/IP 계층 올라감
   5. server 가 client의 요청 데이터 처리하여 응답
   6. server TCP/IP 내려감
   7. server와 client 사이 네트워크
   8. client TCP/IP 계층 올라감
   9. 브라우저 수신 
5. OSI 7계층
   1. 응용계층
   2. Presentation 
   3. Session
   4. Transport
   5. Network
   6. data link
   7. phyisal
6. TCP/IP 4계층
   1. 응용계층
   2. TCP
   3. IP
   4. 네트워크 접근


### OS

1. Thread vs Process

   1. Process
      1. 실행되는 프로그램
      2. 구성 요소 : PCB, 데이터, 힙, 스택
      3. context switch를 통해 프로세스 간 전환 -> 시스템 부하 큼
      4. 상태
         1. 생성
         2. 준비 - 대기 큐
         3. 실행 - dispatch 된 프로세스 사용
         4. 대기 - I/O 발생 등
         5. 완료
      5. 사용 예: 구글 크롬, apache web server

   2. Thread
      1. 독립된 하나의 제어 흐름
      2. 구성 요소 : 스레드 ID, 레지스터 집합, 스택
      3. 경량화된 문맥전환을 사용하여 시스템 부하 적음
      4. 프로세스는 최소 하나를 가짐(main thread)
      5. 종류 
         1. 사용자 수준 쓰레드 : 응용 프로그램에서 사용됨
         2. 커널 수준 쓰레드 : 운영체제의 커널에 의해 운용됨
      6. 사용 예 : 대부분의 응용 프로그램

2. PCB
   1. 운영체제가 `프로세스 관리를 위해 필요한 정보`를 담고 있는 자료 구조
   2. `프로세스 생성시 만들어지고`, `메인 메모리에 유지`
   3. 담긴 정보
      1. PID
      2. 프로세스 상태
      3. 프로그램 카운트
      4. 레지스터 저장 영역
      5. 프로세스 스케줄링 정보
      6. 계정 정보
      7. 입출력 상태 정보
      8. 메모리 관리 정보 
      9. ....

3. 컨텍스트 스위칭

4. 프로세스 동기화

5. 교착상태(Dead lock)
   
   1. 교착상태 조건
      1. 상호배제 : 자원을 배타적으로 점유
      2. 점유 대기 : 한 프로세스가 자원을 점유하고 있으면서 또 다른 자원을 요청하여 대기하고 있는 상태
      3. 비선점 : 오직 점유한 프로세스만 해제 가능
      4. 순환 대기 : 두 개 이상의 프로세스 간 점유와 대기가 원형으로 구성된 상태
   
   2. 교착상태 해결방법
      1. 예방 : 상호배제를 제외한 나머지 교착상태 발생 조건을 위배하는 방안. 점유 자원 해제 후 새 자원 요청
      2. 회피 : 
         1. 안전한 상태를 유지할 수 있는 요구만 수락
         2. 프로세스별 자원 최대요구량 확보
         3. 은행가 알고리즘
      3. 탐지 : 
         1. 감시 알고리즘으로 교착상태 검사
         2. 자원 할당 그래프
      4. 복구 : 
         1. 교착상태가 없어질 때까지 순차적으로 kiil
         2. 프로세스 kill, 자원 선점

6. 세마포어와 뮤텍스

   1. 세마포어
      1. 여러개의 프로세스가 critical section에 진입 가능
      2. 이진 세마포어는 뮤텍스와 비슷

   2. 뮤텍스
      1. critical section에 하나의 프로세스만 진입 가능
      2. 진입한 프로세스만 lock 해제 가능

7. 메모리 관리 방법

   1. 페이징
      1. fixed size
      2. 내부 단편화 발생

   2. Segment
      1. 논리적 단위
      2. 외부 단편화 발생

   3. 페이징 + Segment
      1. segment를 fixed size로 분리

   4. 페이지 기법의 문제점 - 스레싱(Thrashing)
      1. 계속적으로 페이지 부재가 발생하여 프로세스의 실제 처리 시간 보다 페이지 교체 시간이 더 많아지는 현상
      2. 기억장치 접근이 증가하여, 시스템의 성능 및 처리율 저하
      3. 해결 방안
         1. 위킹 세트 : 많이 참조하는 페이지들의 집합을 메모리에 계속 상주 시킴 -> page hit 올림
         2. 페이지 부재 빈도(PFP)
            1. 페이지 부재 비율에 따라 페이지 프레임 개수를 조절

   5. 지역성
      1. 일부 페이지만 집중적으로 참조하는 특성
      2. 참조 지역성
         1. 시간 지역성 : 빠른 시간에 다시 참조될 확률이 높은 특성(ex. loop)
         2. 공간 지역성 : 참조된 메모리 근처의 메모리 참조하는 특성(ex. 배열 순회)

8. 가상메모리

   1. 물리 메모리 크기의 한계를 극복하기 위해 나온 메모리 추상화 기술

   2. 가상 메모리의 핵심
      1. 필요한 부분만 메모리에 적재(부분적재)
      2. 적재 여부를 페이지테이블에 레코드별로 유효 비트를 가지고 판단

   3. 페이징과 스와핑을 합쳐놓은 형태
      1. 메모리를 페이지 단위로 나누어 페이지 테이블을 통해 물리 메모리에 맵핑을 하는데, 필요한 페이지만을 스와핑을 통해 메모리에 올리고 나머지는 하드디스크에 두는 관리 방식

   4. 요구페이징 
      1. 현재 필요한 페이지만 메모리에 올리는 것
      2. page fault 가 발생하면 그 때 트랩을 걸어 해당 페이지를 적재
   
   5. TLB
      1. 가상 메모리 주소를 물리적 주소로 변환하는 속도를 높이기 위해 사용하는 캐시
      2. 최근에 일어난 가상 메모리와 물리 주소의 변환 테이블로 관리
      3. CPU가 가상 주소를 가지고 메모리에 접근하려고 할 때 우선은 TLB에 접근하여 가상 주소에 해당되는 물리 주소를 찾고, 만약 TLB에 매핑이 존재하지 않는다면 MMU가 페이지 테이블에서 해당되는 물리 주소로 변환한 후 메모리에 접근하게 됨.
   
   6. MMU
      1. 특수 메모리 관리 하드웨어
      2. MMU는 가상주소를 물리주소로 변환

9. 프로세스 스케줄링

   1. 선점형
      1. RR
      2. SRT
      3. MLQ(다단계 큐 스케줄링)
      4. MLFQ(다단계 피드백 큐 스케줄링)

   2. 비선점형
      1. 우선순위
      2. Deadline
      3. FCFS
      4. SJF
      5. HRN

   3. 기아 현상(starvation)
      1. 무한정 기다리는 현상
      2. aging 처리하여 우선순위 올림

### Auth
1. Authentication : 로그인
2. Authorization : 권한

3. [Oauth2](https://auth0.com/intro-to-iam/what-is-oauth-2/)
   1. 인증 프로토콜이 아니라 인가 표준 프로토콜 
   2. 애플리케이션이 사용자를 대신하여 다른 웹 앱에서 호스팅하는 리소스에 액세스할 수 있도록 설계된 표준
   3. Oauth2 : Open Authorization의 약자
   4. 장치에 대한 특정 권한 부여 흐름을 제공하는 동시에 클라이언트 개발자의 단순성에 초점을 맞추고 있습니다. 
   5. IETF OAuth 워킹 그룹 내에서 개발되고 있다.
   6. 액세스 토큰 사용
      1. 액세스 토큰은 최종 사용자를 대신하여 리소스에 액세스할 수 있는 권한을 나타내는 데이터 조각입니다. 
      2. 액세스 토큰에 대한 특정 형식을 정의하지 않습니다. 보안상의 이유로 액세스 토큰에는 만료일이 있을 수 있습니다.
         1. JWT(JSON Web Token) 형식이 자주 사용됩니다. 토큰 발급자는 토큰 자체에 데이터를 포함할 수 있습니다. 

4. Jwt(Json Web Token)
   1. 두 당사자 간의 클레임을 안전하게 표현하기 위한 개방형 업계 표준 RFC 7519 방법입니다.
   2. base64UrlEncode(header).base64UrlEncode(payload).HMACSHA256(base64UrlEncode(header).base64UrlEncode(payload), 256-bit-secret)
   3. 구조
      1. header: ALGORITHM & TOKEN TYPE
      2. payload : data
         1. 등록된 클레임(registered)
            1. iss
            2. sub
            3. aud
            4. exp
            5. nbf
            6. iat
            7. jti
         2. 공개 클레임(public) : 충돌이 방지된 (collision-resistant) 이름 사용
         3. 비공개 클레임(private) : 양 측간에 (보통 클라이언트 <->서버) 협의하에 사용되는 클레임
      3. SIGNATURE(메시지 인증 코드)
   4. JWT is a parent of JWS and JWE.
      1. JWS가 일반적으로 사용하는 JWT
      2. JSON Web Encryption (JWE)
         1. JSON 데이터 구조 및 base64url 인코딩을 사용하여 암호화된 콘텐츠를 나타냅니다.
         2. BASE64URL(UTF8(JWE Protected Header)).BASE64URL(JWE Encrypted Key).BASE64URL(JWE Initialization Vector).BASE64URL(JWE Ciphertext).BASE64URL(JWE Authentication Tag)

### ETC
1. Restful API
   1. REST 아키텍처의 제약 조건을 준수하는 애플리케이션 프로그래밍 인터페이스를 뜻
   2. REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일
   
   3. URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용
   
   4. 특징
      1. HTTP를 통해 관리되는 클라이언트-서버 아키텍처
      2. 클라이언트-서버 상호 작용을 간소화하는 캐시 가능 데이터
      3. Stateless(무상태) : 요청 간에 클라이언트 정보가 저장되지 않으며, 각 요청이 분리되어 있고 서로 연결되어 있지 않음
      4. 수신한 표현을 통해 클라이언트가 리소스를 조작할 수 있어야 합니다(이렇게 할 수 있는 충분한 정보가 표현에 포함되어 있기 때문)
      5. 클라이언트에 반환되는 자기 기술적(self-descriptive) 메시지에 클라이언트가 정보를 어떻게 처리해야 할지 설명하는 정보가 충분히 포함되어야 합니다.
      6. 하이퍼미디어: 클라이언트가 리소스에 액세스한 후 하이퍼링크를 사용해 현재 수행 가능한 기타 모든 작업을 찾을 수 있어야 합니다.
      7. 요청된 정보를 검색하는 데 관련된 서버(보안, 로드 밸런싱 등을 담당)의 각 유형을 클라이언트가 볼 수 없는 계층 구조로 체계화하는 계층화된 시스템.
      8. 코드 온디맨드(선택 사항): 요청을 받으면 서버에서 클라이언트로 실행 가능한 코드를 전송하여 클라이언트 기능을 확장할 수 있는 기능. 
   
   5. 장/단점
      1. 장점
         1. 다양한 client device 대응
         2. HTTP 인프라 그대로 사용
         3. 의도하는 바를 쉽게 파악
         4. 사용하기 쉽다
      2. 단점
         1. 표준 X
         2. Client에서 호출해야 할 API 수가 많아 지는 경향이 있다.
   
   6. Method 종류 
      1. Get : 조회
      2. Post : 생성
      3. PUT : 전체 수정, 자원 없으면 생성
      4. Patch : 부분 수정
      5. Delete : 삭제
      6. Head : header 정보 조회

   7. 상태코드 종류
      
      1. 1xx(정보) : 요청을 받았으며 프로세스를 계속 진행합니다.
         - 서버가 요청을 받았으며, 서버에 연결된 클라이언트는 작업을 계속 진행하라는 의미입니다. 해당 코드는 HTTP 1.0에서 지원되지 않습니다.
         
         - 100 Continue 
           - 진행 중임을 의미
           - 진행상태에 문제가 없으며, 클라이언트가 계속해서 요청을 하거나 이미 요청을 완료한 경우에는 무시해도 되는 것을 알려줍니다.
         
         - 101 Switching Protocol 
           - 클라이언트가 보낸 Upgrade 요청 헤더에 대한 응답에 들어가며, 서버에서 프로토콜을 변경할 것임을 알려줍니다. 
           - 해당 코드는 Websocket 프로토콜 전환 시에 사용됩니다.

      2. 2xx(성공) : 요청을 성공적으로 받았으며 인식했고 수용하였습니다.
         
         - 200 OK : 요청 성공
         
         - 201 Created : 요청 성공, 그 결과로 새로운 리소스가 생성 (POST/PUT 요청)
         
         - 202 Accepted 
           - 요청을 수신하였지만, 그에 요청에 대한 결과는 즉시 주지 않음 
           - 비동기 처리
           - 다른 프로세스에서 처리 또는 서버가 요청을 다루고 있거나 배치 프로세스를 하고 있는 경우를 위해 만들어졌습니다.
         
         - 204 No Content 
           - 요청에 대해서 보내줄 수 있는 콘텐츠가 없지만, 헤더는 의미있을 수 있습니다. 
         
         - 205 Reset Content 
           - 요청을 완수한 이후에 사용자 에이전트에게 이 요청을 보낸 문서 뷰를 리셋하라고 알려줍니다.
         
         - 206 Partial Content 
           - 클라이언트에서 복수의 스트림을 분할 다운로드를 하고자 범위 헤더를 전송했기 때문에 사용됩니다. 
           - 클라이언트가 이어받기를 시도하면 웹서버가 이에 대한 응답코드로 '206 Partial Content'와 함께 Range 헤더에 명시된 데이터의 부분(byte)부터 전송을 시작합니다.

      3. 3xx(리다이렉션) : 요청 완료를 위해 추가 작업 조치가 필요합니다.
         
         - 301 Moved Permanently
           - 요청한 리소스의 URI가 변경되었음을 의미합니다. 
           - 새로운 URI가 응답에서 아마도 주어질 수 있습니다.
         
         - 302 Found
           - 요청한 리소스의 URI가 일시적으로 변경되었음을 의미
           - 새롭게 변경된 URI는 나중에 만들어질 수 있습니다. 그러므로, 클라이언트는 향후의 요청도 반드시 동일한 URI로 해야합니다.
         
         - 303 See Other
           - 클라이언트가 요청한 리소스를 다른 URI에서 GET 요청을 통해 얻어야 할 때, 서버가 클라이언트로 직접 보내는 응답입니다.
         
         - 304 Not Modified
           - 캐시 목적으로 사용
           - 클라이언트에게 응답이 수정되지 않았음을 알려주며, 그러므로 클라이언트는 계속해서 응답의 캐시된 버전을 사용할 수 있습니다.
         
         - 307 Temporary Redirect 
           - 요청한 리소스가 다른 URI에 있으며, 이전 요청과 동일한 메소드를 사용하여 요청해야 할 때, 서버가 클라이언트에 이 응답을 직접 보냅니다.
           - 302 Found HTTP 와 동일한 의미를 가지고 있으며, 사용자 에이전트가 반드시 사용된 HTTP 메소드를 변경하지 말아야 하는 점만 다릅니다.
         
         - 308 Permanent Redirect 
           - 리소스가 HTTP 응답 헤더의 Location:에 명시된 영구히 다른 URI에 위치하고 있음을 의미
           - 301 Moved Permanently 와 동일한 의미를 가지고 있으며, 사용자 에이전트가 반드시 HTTP 메소드를 변경하지 말아야 하는 점만 다릅니다. 

      4. 4xx(클라이언트 오류) : 요청의 문법이 잘못되었거나 요청을 처리할 수 없습니다.
         
         - `400 Bad Request` 
           - 잘못된 문법으로 인하여 서버가 요청를 이해할 수 없음을 의미

         - `401 Unauthorized` 
           - 비록 HTTP 표준에서는 '미승인(unauthorized)'를 명확히 하고 있지만, 의미상 이 응답은 '비인증(unauthenticated)'를 의미
           - 클라이언트는 반드시 스스로를 인증해야 합니다.

         - `403 Forbidden` 
           - 클라이언트는 콘텐츠에 접근할 권리를 가지고 있지 않습니다. 
           - 401과 다른 점은 서버가 클라이언트가 누구인지 알고 있습니다.

         - `404 Not Found` 
           - 요청받은 리소스를 찾을 수 없습니다. 
             - 요청 포맷이 존재하지 않을 경우(URl, Method .. )
             - 요청 포맷은 존재하나 요청 데이터가 없는 경우
           - 서버들은 인증받지 않은 클라이언트로부터 리소스를 숨기기 위하여 이 응답을 403 대신에 전송할 수도 있습니다. 

         - `405 Method Not Allowed` 
           - 요청한 메소드는 서버에서 알고 있지만, 제거되었고 사용할 수 없습니다. 
           - 예를 들어, 어떤 API에서 리소스를 삭제하는 것을 금지할 수 있습니다. 
           - `필수적인 메소드인 GET과 HEAD는 제거될 수 없으며, 이 에러 코드를 리턴할 수 없습니다.`

         - 406 Not Acceptable 
           - 서버가 서버 주도 콘텐츠 협상을 수행한 후, 사용자 에이전트에서 정해준 규격에 따른 어떠한 콘텐츠도 찾지 않았을 때, 웹서버가 보냅니다.

         - 407 Proxy Authentication Required
           - 401과 비슷하지만 프록시에 의해 완료된 인증이 필요합니다.

         - 408 Request Timeout 
           - 요청을 한 지 시간이 오래된 연결에 일부 서버가 전송하며, 어떤 때에는 이전에 클라이언트로부터 어떠한 요청이 없었다고 하더라도 보내지기도 합니다. 
           - 서버가 사용되지 않는 연결을 끊고 싶어하는 것을 의미합니다. 
           - 몇몇 브라우저에서 빈번하게 보이는데 Chrome, Firefox 27+, 또는 IE 9와 같은 웹서핑 속도를 올리기 위해 HTTP 사전 연결 메카니즘을 사용하는 브라우저들이 해당됩니다. 
           - 일부 서버는 이 메시지를 보내지 않고 연결을 끊어버리기도 합니다.

         - 409 Conflict 
           - 요청이 현재 서버의 상태와 충돌될 때 보냅니다.

         - 410 Gone 
           - 요청한 콘텐츠가 서버에서 영구적으로 삭제되었으며, 전달해 줄 수 있는 주소 역시 존재하지 않을 때 보냅니다. 
           - 클라이언트가 그들의 캐시와 리소스에 대한 링크를 지우기를 기대합니다. 
           - HTTP 기술 사양은 이 상태 코드가 '일시적인, 홍보용 서비스'에 사용되기를 기대합니다. 
           - API는 알려진 리소스가 이 상태 코드와 함께 삭제되었다고 강요해서는 안된다.

         - 411 Length Required
           - 서버에서 필요로 하는 Content-Length 헤더 필드가 정의되지 않은 요청이 들어왔기 때문에 서버가 요청을 거절합니다.

         - 412 Precondition Failed
           - 클라이언트의 헤더에 있는 전제조건은 서버의 전제조건에 적절하지 않습니다.

         - `413 Payload Too Large`
           - 요청 엔티티는 서버에서 정의한 한계보다 큽니다. 서버는 연결을 끊거나 혹은 Retry-After 헤더 필드로 돌려보낼 것이다.

         - `414 URI Too Long`
           - 클라이언트가 요청한 URI는 서버에서 처리하지 않기로 한 길이보다 깁니다.

         - `415 Unsupported Media Type`
           - 요청한 미디어 포맷은 서버에서 지원하지 않습니다. 서버는 해당 요청을 거절할 것입니다.

         - `416 Requested Range Not Satisfiable`
           - Range 헤더 필드에 요청한 지정 범위를 만족시킬 수 없습니다. 
           - 범위가 타겟 URI 데이터의 크기를 벗어났을 가능성이 있습니다.

         - 417 Expectation Failed
           - Expect 요청 헤더 필드로 요청한 예상이 서버에서는 적당하지 않음을 알려줍니다.

         - 421 Misdirected Request
           - 서버로 유도된 요청은 응답을 생성할 수 없습니다. 
           - 이것은 서버에서 요청 URI와 연결된 스킴과 권한을 구성하여 응답을 생성할 수 없을 때 보내집니다.

         - `426 Upgrade Required`
           - 서버는 지금의 프로토콜을 사용하여 요청을 처리하는 것을 거절하였지만, 클라이언트가 다른 프로토콜로 업그레이드를 하면 처리를 할지도 모릅니다. 
           - 서버는 Upgrade 헤더와 필요로 하는 프로토콜을 알려주기 위해 426 응답에 보냅니다.

         - 428 Precondition Required
           - 오리진 서버는 요청이 조건적이어야 합니다. 
           - 클라이언트가 리소스를 GET해서, 수정하고, 그리고 PUT으로 서버에 돌려놓는 동안 서드파티가 서버의 상태를 수정하여 발생하는 충돌인 '업데이트 상실'을 예방하기 위한 목적입니다.

         - `429 Too Many Requests`
           - 사용자가 지정된 시간에 너무 많은 요청을 보냈습니다("rate limiting").

         - `431 Request Header Fields Too Large` 
           - 요청한 헤더 필드가 너무 크기 때문에 서버는 요청을 처리하지 않을 것입니다. 
           - 요청은 크기를 줄인 다음에 다시 전송해야 합니다.

         - 451 Unavailable For Legal Reasons
           - 사용자가 요청한 것은 정부에 의해 검열된 웹페이지와 같은 불법적인 리소스입니다.


      5. 5xx(서버 오류) : 서버가 명백히 유효한 요청에 대한 충족을 실패했습니다.

         - `500 Internal Server Error`
           - 서버에 문제가 있음을 의미하지만 문제에 대해 구체적으로 설명할 수 없습니다.

         - 501 Not Implemented
           - 서버가 요청을 이행하는 데 필요한 기능을 지원하지 않음을 나타냅니다.

         - 502 Bad Gateway
           - 서버가 게이트웨이로부터 잘못된 응답을 수신했음을 의미
           - 인터넷상의 서버가 다른 서버로부터 유효하지 않은 응답을 받은 경우 발생

         - `503 Service Unavailable`
           - 서버가 요청을 처리할 준비가 되지 않았습니다. 
           - 일반적인 원인은 유지보수를 위해 작동이 중단되거나 과부하가 걸린 서버입니다. 
           - 이 응답과 함께 문제를 설명하는 사용자 친화적인 페이지가 전송되어야 한다는 점에 유의하십시오. 
           - 이 응답은 임시 조건에 사용되어야 하며, `Retry-After:` HTTP 헤더는 가능하면 서비스를 복구하기 전 예상 시간을 포함해야 합니다. 
           - 웹마스터는 또한 이러한 일시적인 조건 응답을 캐시하지 않아야 하므로 이 응답과 함께 전송되는 캐싱 관련 헤더에 대해서도 주의해야 합니다.

         - 504 Gateway Timeout
           - 웹페이지를 로드하거나 브라우저에서 다른 요청을 채우려는 동안 한 서버가 액세스하고 있는 다른 서버에서 적시에 응답을 받지 못했음을 의미합니다. 
           - 이 오류 응답은 서버가 게이트웨이 역할을 하고 있으며 적시에 응답을 받을 수 없을 경우 주어집니다. 
           - 이 오류는 대게 인터넷상의 서버 간의 네트워크 오류이거나 실제 서버의 문제입니다. 
           - 컴퓨터, 장치 또는 인터넷 연결에 문제가 아닐 수 있습니다.

         - 505 HTTP Version Not Supported
           - 서버에서 지원되지 않는 HTTP 버전을 클라이언트가 요청하였습니다. 
           - 대부분의 웹 브라우저는 웹 서버가 1.x 버전의 HTTP 프로토콜을 지원한다고 가정합니다. 
           - 웹 서버 소프트웨어에서 지원하는 HTTP 버전을 확인해 보아야 합니다.

         - 506 Variant Also Negotiates
         - 507 Insufficient Storage
         - 511 Network Authentication Required
           - 클라이언트가 네트워크 액세스를 얻기 위해 인증할 필요가 있음을 나타냅니다.

2. 기본 자료구조
   
   1. 선형구조
      1. array
      2. linkedlist
         1. 단순
         2. 이중
         3. 원형
      3. queue
         1. priority queue
      4. stack
      5. deque
         1. 앞과 뒤에서 데이터를 처리할 수 있는 양방향 자료형이다. 
         2. 양방향이기 때문에 스택(Stack)처럼 써도 되고 큐(Queue)처럼 써도 된다.
   
   2. 비선형 구조
      1. tree
         1. binary tree
         2. b-tree
         3. red-black tree
      2. graph
         1. 방향 그래프
         2. 무방향 그래프
      3. hashTable

3. TDD
   1. 정의
      1. 테스트를 먼저 만들고 테스트를 통과하기 위한 코드를 작성하는 방법
   
   2. [장/단점](https://www.geeksforgeeks.org/advantages-and-disadvantages-of-test-driven-development-tdd/)
      1. 장점
         1. 필요한 코드만 작성
         2. 더 많은 모듈식 디자인
         3. 유지보수 용이
         4. 더 쉽게 리팩토링
      2. 단점
         1. 학습 곡선
         2. 더 오래걸리는 BUILD 시간
         3. 테스트 환경 구성 어려움
   
   3. 나의 선호 테스트 방식
      1. BDD
      2. 프로그램 layer 별 단위 테스트
   
   4. TDD vs BDD
      1. BDD 시나리오 기반 테스트 개발 방식(given-when-then)
         1. TDD 확장 버전

4. 디자인 패턴
   
   1. Creational
      1. Factory : 인스턴스를 직접 생성해내지 않고, 공장에서 제공하는 메쏘드를 통해 생성
      2. Factory Method : 객체를 생성하기 위한 인터페이스를 정의하여 어떤 클래스가 인스턴스화 될 것인지는 서브 클래스가 결정하도록 하는 패턴
      3. Abstract Factory : 생성군들을 하나의 모아놓고 팩토리 중에서 선택하게 하는 패턴
      4. Builder : 생산 단계를 캡슐화 하여 구축 공정을 동일하게 이용하도록 하는 패턴
         1. 생성자의 파라미터가 많을때
      5. Singleton : 하나의(Single) 인스턴스만 생성하고, 이후에는 이 인스턴스를 참조
      6. Prototype : 기존의 인스턴스를 그대로 복제(clone) 하여 새로운 객체를 생성하는 방법
   
   2. Structural
      1. Adapter : 인터페이스가 호환되지 않는 클래스들을 함께 이용할 수 있도록, 타 클래스의 인터페이스를 기존 인터페이스에 덧씌운다.
      2. Proxy : 접근 조절, 비용 절감, 복잡도 감소를 위해 접근이 힘든 객체에 대한 대역을 제공한다.
         1. 핵심 로직에 영향을 주지 않으면서, 부가적인 작업이 필요할때
      3. Facade : 많은 분량의 코드에 접근할 수 있는 단순한 인터페이스를 제공한다.
      4. Decorator : 기존 객체의 매서드에 새로운 행동 추가
      5. Bridge : 추상과 구현을 분리
      6. Flyweight : 다수의 유사한 객체를 생성·조작하는 비용을 절감할 수 있다.
      7. Composite : 개별 객체와 복합 객체를 클라이언트에서 동일하게 사용하도록 하는 패턴
         1. 파일과 디렉토리 관계 - 파일과 디렉토리의 추상화를 만들어서 상속 받게 하고 동일 인터페이스로 파일과 디렉토리를 다룬다.
   
   3. Behavioral
      1. Strategy : 다양한 알고리즘 캡슐화하여 알고리즘 대체가 가능하도록 한 패턴
      2. State : 객체 내부 상태에 따라서 행위 변경
      3. Template Method : 알고리즘 골격의 구조를 정의한 패턴
      4. Command : 요청 자체를 캡슐화하여 파라미터로 넘기는 패턴
      5. Chain of Responsibility : 책임들이 연결되어 있어 내가 책임을 못 질 것 같으면 다음 책임자에게 자동으로 넘어가는 구조
      6. Observer : 생산자에 소비자 등록 후 생산자의 상태가 변경되면 소비자에게 알려주는 패턴
      7. Memento : 상태 값을 저장해 두었다가 복구
      8. Mediator : 객체 간 상호작용을 중재자를 통해서만 할 수있게 하는 패턴
      9. Visitor : 
         1.  실제 로직을 가지고 있는 객체가 로직을 적용할 객체를 방문하면서 실행하는 패턴
         2.  로직과 구조를 분리하는 패턴
      10. iterator : 집합 데이터의 일관된 순회 방법 제공 패턴

5. 객체지향
   1. 프로그래밍 패러다임 중 하나
   2. 상태와 행위를 가진 객체들을 만들고 그 객체들 간의 유기적인 상호작용을 통해 로직을 구성하는 프로그래밍 방법
   
   3. 장/단점
      
      1. 장점
         1. 재사용성이 높아진다.
         2. 유지보수가 쉽다.
         3. 코드가 간결해진다.
      
      2. 단점
         1. 처리 시간이 비교적 오래 걸린다.
         2. 프로그램을 설계할 때 많은 고민과 시간을 투자해야한다.
   
   4. 객체지향 4가지 특징
      
      1. 추상화 (Abstraction)
         1. 공통적인 특징을 뽑아낸다.
      
      2. 캡슐화 (Encapsulation)
         1. 외부에서 직접 접근하지 못하도록 은닉하는 것
      
      3. 상속성 (Inheritance)
         1. 상위 클래스의 자료와 연산을 하위 클래스가 물려받아 이용할 수 있게 하는 것
      
      4. 다형성 (Polymorphism)
         1. 하나의 메소드나 클래스가 상황에 따라 다양한 동작하는 것
         2. 일반적으로 오버라이딩이나 오버로딩을 의미
   
   5. 객체지향 5대 원칙 : SOLID
      
      1. SRP(Single Responsibility Principle)
         1. 한 클래스/메소드는 하나의 책임만 가져야 한다.
      
      2. OCP(Open/Closed Principle)
         1. 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.
      
      3. LSP(Liskov’s Substitution Principle)
         1. 부모-자식 클래스 관계에서 자식은 부모를 대신 할 수 있어야 하는데, 자식은 부모의 설계 의도를 지켜야한다.
      
      4. ISP(Interface Segregation Principle)
         1. 클라이언트가 미구현하는 함수가 없게 인터페이스 분리
         2. 클라이언트는 사용하지 않을 불필요한 방법을 구현하도록 강요되어서는 안됩니다.
      
      5. DIP(Dependency Inversion Principle)
         1. 구체화가 아닌 추상화에 의존

6. 동등성(equality) vs 동일성(identity)
   
   - 동등성
     - 실제 인스턴스는 다를 수 있지만 인스턴스가 가지고 있는 값이 같다.
     - 자바에서 동등성 비교는 equals 메소드를 구현해야 한다.
   
   - 동일성
     - 실제 인스턴스가 같다.
     - 따라서 참조하는 값을 비교하는 == 비교의 값과 같다.

7.  성능 테스트 방법(부하 테스트)

8.  정렬 종류
    1. quick sort
       1. pivot의 값을 기준으로 값이 작은 배열과 큰 배열로 정렬
       2. Top-Down 방식
       3. 시간복잡도  
          1. 평균 : O(nlogn)
          2. 최악 : O(n^2) - 이미 거의 정렬된 상태 일 경우
       4. Not Stable
       5. swap를 이용해서 추가 메모리 공간이 거의 필요하지 않음
    2. merge sort
       1. 정확히 반으로 나누면서 정렬과 병합을 반복하는 형식
       2. Bottom-Up 방식
       3. 시간복잡도  
          1. 평균 : O(nlogn)
       4. Stable
       5. 추가 메모리 공간 필요
       6. 일관된 속도를 보장

9.  quick sort VS merge sort
    
    1. 공통점 : 
        1. 평균 시간복잡도 : O(nlogn)
        2. 분할 정복(divide and conquer)
    
    2. 차이점 : 
       1. 추가적인 메모리 공간 필요 여부
       2. 참조 지역성 사용여부
          1. 정렬하려고 하는 데이터들이 다른 페이지로 이동하는 것 없이, 자신의 페이지에서 계속 있는게 좋다. 다른 캐쉬에 없는 페이지로 이동하면 page cache hit 비율이 떨어지게 된다. 그래서 결국 physical memory로 접근을 해야 하기 때문에 시간이 상대적으로 오래 걸린다. 만약 자신의 페이지에 계속 있는다면, cache에서 반복적으로 접근하기 때문에 시간이 덜 걸린다. 결국 데이터가 이동하지 않을 수록 좋다. 위 코드에서 알수 있듯이 Quick Sort는 Merge Sort에 비해 pivot에 의한 분할은 했지만 데이터가 존재하는 위치는 변하지 않는다. 따라서 제자리정렬이라 할수있으며 지역성의 원리에 따라 더 빠른 성능을 보이기도 한다는 것이다.

10. 부하분산 또는 로드 밸런싱(Load balancing) 종류와 알고리즘
    
    1. 둘 혹은 셋이상의 컴퓨터 자원들에게 작업을 나누는 것을 의미한다. 즉 여러 서버가 분산 처리 하는것을 로드 밸런싱이라고 합니다. 
    2. 로드 밸런서 : 로드 밸런싱 기술을 제공하는 서비스 또는 장치
    
    3. 종류
       1. L2 : Data link 계층을 사용, Mac주소 기반 부하 분산	 
       2. L3 : Network 계층을 사용, IP주소 기반 부하 분산
       3. L4 : Transport 계층을 사용, 포트 번호 기반 부하 분산
       4. L7 : Application 계층을 사용, URL 또는 HTTP 헤더 기반 부하 분산
  
    4. algorithm 종류
       
       1. Round Robin
          1. 요청이 들어오는 대로 서버마다 균등하게 요청을 분배
          2. 서버의 성능이 동일하고 처리 시간이 짧은 애플리케이션의 경우, 균등하게 분산이 이루어지기 때문에 이 방식을 사용
       
       2. Weighted Round Robin Scheduling
          1. 각 서버에 가중치를 부여할 수 있으며, 지정한 정숫값을 통해 처리 용량을 지정
          2. 서버 스팩이 서로 상이한 경우 사용
       
       3. Least Connection
          1. 서버마다 연결된 커넥션이 몇개인지 체크하여 커넥션이 가장 적은 서버로 요청을 분배하는 방식
       
       4. Fastest Response Time
          1. 서버가 요청에 대해 응답하는 시간을 체크하여 가장 빠른 서버로 요청을 분배
       
       5. Source Hash Scheduling(=? stick session?)
          1. 사용자의 IP를 해싱한 후 그 결과에 따라 서버로 요청을 분배
          2. 사용자의 IP는 고정되어 있기 때문에 항상 같은 서버로 연결된다는 보장

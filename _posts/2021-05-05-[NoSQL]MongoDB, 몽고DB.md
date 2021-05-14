MongoDB
=====

<br>

클라우드 컴퓨팅 환경이 생겨나고 그 안에서 방대한 양의 빅데이터가 쏟아짐에 따라 빅데이터를 저장하고 관리하는데 여러 문제점이 발생하고 있었다. RDB(관계형 데이터베이스)에서 빅데이터를 처리하기에 데이터의 크기와 처리하는데 걸리는 속도에 한계점이 있었고, 이를 해결하기 위해 NoSQL이라는 새로운 데이터 저장 기술이 등장했다.  
NoSQL은 정확한 의미로 Non Relational Operational Database SQL로 관계형 데이터베이스가 아닌 SQL이라는 의미를 갖고있으며 관계형 데이터베이스가 아니기 때문에 NoSQL만의 여러 장점이 존재한다. 개인적으로 NoSQL의 가장 큰 장점은 수평확장이라 생각한다. 확장은 크게 수직(Vertical) 확장과 수평(Horizontal) 확장으로 구분하는데 수직 확장은 데이터베이스 서버의 크기를 증가시켜 성능 향상을 하는 것이고, 수평 확장은 데이터베이스 서버의 수를 증가시켜 데이터베이스를 여러개의 서버로 분산시키는 것이다.
> 수직 확장과 수평 확장을 스케일 업(Scale Up), 스케일 아웃(Scale Out)이라 부르기도 한다.

![mongodb2](https://user-images.githubusercontent.com/82218035/117109223-4ac95780-adbf-11eb-83ff-0f5579b272ad.png)

<br>

NoSQL은 수평 확장을 통해 방대한 양의 빅데이터를 효율적으로 처리할수있다. 빅데이터는 비정형 데이터가 주를 이루고 있기 때문에 비정형 데이터를 정형화된 데이터 구조의 관계형 데이터베이스에 저장하여 체계적으로 관리하는 것보다 데이터를 어떻게 효율적으로 읽고, 쓰기의 작업을 하느냐가 더 중요하다. 빅데이터의 이러한 활용 목적 때문에 효율적인 처리가 가능한 분산 처리 방법이 필요했고, 분산 처리 시스템을 적용하기 위해 수평 확장이 가능한 NoSQL로 빅데이터를 관리하고 있다.

<br>

![mongodb1](https://user-images.githubusercontent.com/82218035/117109251-574db000-adbf-11eb-86de-9acaf59cf7fd.png)

NoSQL은 네 종류로 구분된다. 키-값(Key-Value) 형식으로 데이터를 저장하는 Key-Value Store, 컬럼 지향형(Column-Oriented) 구조의 Wide-Column-Store, 그래프 구조를 사용하는 Graph-DataBase, 마지막으로 도큐먼트 데이터베이스(Document-Database)가 있다.

<br>

<img width="439" alt="스크린샷 2021-05-05 오후 6 11 18" src="https://user-images.githubusercontent.com/82218035/117119659-5a4f9d00-adcd-11eb-9530-d149086c9834.png">

MongoDB는 Document-Database로 Document와 Collection으로 이뤄졌다. Key-Value형식인 json 데이터를 하나의 문서(Document)로 저장한다. 데이터가 모여 하나의 Document를 이루고, 여러개의 Document가 모여 하나의 Collection을 형성한다. 관계형 데이터베이스에 빗대어보면 Document는 데이터를 구분시켜주는 테이블의 PK이고 Collection은 테이블과 비슷하다.  
MongoDB의 Collection은 관계형 데이터베이스의 테이블과 다르게 스키마가 없어 서로 다른 타입의 데이터를 저장하는데 제약사항이 따르지 않는다. 스키마가 없기 때문에 장점으로 데이터베이스의 유연한 확장과 스케일 업이 가능하지만, 다르게 생각해보면 스키마가 없어 Collection 간의 Join이 불가능 하다는 단점이 있다.   

<br>

>MongoDB, GridFS  
MongoDB는 Document의 최대 크기가 16MB이기 때문에 사이즈가 큰 비정형 데이터를 저장 할 수 있는 파일 시스템으로 GridFS를 제공한다. GridFS는 최대 2GB의 파일까지 저장가능하며, 파일을 256KB로 나누어 저장한다. GridFS에는 파일의 정보를 저장하는 메타데이터 역할의 files와 실질적인 파일의 내용을 저장하는 chunks가 있다.

<br>

###### 결론
- NoSQL은 빅데이터를 처리하기 위해 등장한 데이터 저장 기술이다.
- MongoDB는 Document-Database로 Document와 Collection으로 이뤄졌다.
- MongdoDB는 스키마가 없어 join이 불가능 하지만 스케일 업을 통한 데이터베이스 확장이 가능하다.

<!--
마치 MongoDB 여러 개의 방마다 데이터를 저장하는 하나의 큰 건물과 같다는 생각이 들었다.
각각의 방에는 다양한 데이터가 저장되고 key를 통해 데이터를 찾을 수 있다.


큰 공간에 정리 안된 여러개의 서재
쌓기에는 유리 삭제 시 불리


MongoDB

문서지향 데이터베이스

스키마가 없다

스케일 아웃이 가능하다 (스케일아웃?)

범용 데이터베이스

조인과 트랜잭션이 없다 (트랜잭션?)

낮은 진입장벽

문서(document)는 RDB의 행(Row)이다 (document?)

컬렉션은 테이블이다, 컬렉션은 테이블처럼 이름을 가진다 (컬렉션?)

데이터베이스에서 컬렉션을 그룹지어 놓는다
-->

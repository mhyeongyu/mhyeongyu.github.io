HBase
=======================

<br>

실시간 로그 분석에서는 작지만 대량으로 발생하는 메시지성 데이터를 실시간으로 처리하며, 해당 결과를 인메모리에 저장해 주변 시스템과 빠르게 공유한다. 이때 대량의 메시지 데이터를 영구 저장하기 위해 Hadoop을 직접 이용하지 않는다. 그 이유는 유입된 작은 메시지 한 건을 곧바로 Hadoop에 저장할 경우 한 개의 HDFS 파일이 생성되는데, 초당 수천 건의 트랜잭션이 발생하는 메시지의 경우 파일 개수가 기하급수적으로 늘어나고 이로 인해 Hadoop 클러스터에 지나친 오버헤드가 발생하기 때문이다. 그리고 파일의 내용이 자주 수정되면 파일을 Hadoop에 저장하는 것보다 분산 환경 기반의 DB에 데이터를 저장하고 Query를 이용해 수정, 삭제하는 방식이 더욱 효과적이다. 이러한 문제를 해결하기 위해 중간에 메시지를 특정 크기로 모았다가 한꺼번에 적재하거나 대규모 트랜잭션 데이터를 처리하는데 최적화된 컬럼 지향형 NoSQL DB인 HBase를 사용한다.


![hbase](https://user-images.githubusercontent.com/82218035/116166218-80739e00-a738-11eb-84c8-1d4c3a207f9f.PNG)

![hbase5](https://user-images.githubusercontent.com/82218035/116183928-d147be80-a759-11eb-82c6-c9701b69aa97.PNG)


HBase는 Hadoop 기반의 Column-Oriented NoSQL DB로 Hadoop의 분산파일시스템인 HDFS 위에서 동작하여 HDFS의 가용성과 확장성을 그대로 물려받았다. 데이터는 Key-Value 형식으로 단순하게 구조화되어있으며, HRegion을 통해 수평확장이 가능해 데이터의 양이 증가하면 Node를 추가해주면 된다.  

<br>

![hbase2](https://user-images.githubusercontent.com/82218035/116166239-8a959c80-a738-11eb-8330-0120b915b631.PNG)


HBase는 마스터-슬레이브 구조로 HMaster는 마스터의 역할을 하고, HRegionServer는 슬레이브의 역할을 한다. HMaster는 HBase에 대해 설정한 옵션과 HRegionServer에 대한 정보만을 가지고 있는 서버이다. 그리고 HRegionServer는 HRegion을 관리하며, 데이터 로우에 대한 정보가 저장되어 있다. HRegion은 데이터 사이즈가 저장 가능한 한계치를 초과하면 HRegion은 두 개의 Region으로 분할한다. 클라이언트가 HBase에 데이터를 저장하는 과정은 Zookeeper, HMaster, HRegionServer의 상호작용을 통해 이루어진다. HBase의 Table에 데이터를 저장하기 전 Zookeeper를 통해 HTable의 기본 정보와 HRegion의 위치 정보를 알아내고, 클라이언트가 직접 HRegionServer로 연결되어 HRegion의 MemStore에 데이터를 저장한다. 그리고 MemStore의 데이터는 특정 시점이 되면 영구 저장 영역인 HDFS의 HFile로 이동한다. HBase에서 데이터를 불러오는 과정을 보면 Zookeeper를 통해 RowKey에 해당하는 데이터의 위치 정보를 알아내고 HRegionServer로 연결되어 HRegion의 MemStore에서 데이터를 가져온다. 이때 MemStore에서 데이터가 HDFS의 HFile로 이동한 경우라면 영역을 이동해 데이터를 찾고 가져온다.

<br>

![hbase4](https://user-images.githubusercontent.com/82218035/116166258-984b2200-a738-11eb-83cc-e0a9f023b651.PNG)


HBase의 Table은 크게 RowKey, ColumnFamily, Column, Cell로 이루어져 있다. Column-Oriented Table이기 때문에 기본 단위인 Columns이 모여 ColumnFamily를 구성한다. 그리고 Table의 RowKey는 각각의 Row를 식별가능하게 만들어준다.


![hbase3](https://user-images.githubusercontent.com/82218035/116166321-b3b62d00-a738-11eb-9fb4-68577a70b2a1.PNG)


다음 그림을 보면 우리가 흔히 알고있는 Row-Oriented인 RDBMS와 Column-Oriented의 차이를 파악할수있다. Row-Oriented는 하나의 Table에 모든 정보를 나타내기 때문에 분산처리가 불가능하지만 Column-Oriented는 Table을 여러개로 나눠 원하는 데이터만 저장하거나 가져오는 등의 분산처리가 가능할것이다. 만약 Table의 Column과 Row가 무수히 많다고 가정해보자, 데이터를 조회하기에 Column-Oriented는 데이터의 Volum이 증가할수록 더욱 효율적인 데이터 처리 능력을 보여줄것이다. 일반적인 DB의 Table은 데이터는 Volumn이 크지않아 Row-Oriented 방식을 선호하지만, BigData가 생겨나면서 데이터의 Volumn을 감당하기위해 분산처리가 필요했고, 분산처리 방식에 맞춰 Column-Oriented DB인 HBase를 사용한다고 보여진다.

<br>

결론
- HBase는 BigData를 처리하는데 최적화된 Column-Oriented NoSQL DB이다.
- 데이터 처리는 Zookeeper, HMaster, HRegionServer의 상호작용을 통해 이루어진다
- HBase의 Table은 크게 RowKey, ColumnFamily, Column, Cell로 이루어져 있다.

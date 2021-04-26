Hive
=======================

<br>


Hadoop은 데이터를 탐색, 분석하기 위한 도구로 MapReduce를 주로 이용했다. 하지만 MapReduce는 데이터를 탐색하기 위해 높은 수준의 프로그래밍 기법이 필요했고, 빅데이터를 활용하고자 하는 이들의 접근을 어렵게 만들었다. 이를 해결하기 위해 Facebook에서 보다 쉬운 접근을 위해 SQL과 유사한 방식으로 Hadoop 데이터에 접근 가능한 Hive를 개발했다. Hive는 Hadoop의 HDFS에 저장되어 있는 파일과 Hbase에 적재되어있는 데이터를 SQL로 분석하고 처리하기 위한 환경을 제공하고 현재는 대부분 Hive로 Hadoop의 데이터를 조회하고 분석을 시행하고 있다.



![hive3](https://user-images.githubusercontent.com/82218035/116034396-2aeab300-a69e-11eb-8999-0fc0bb155e1a.PNG)



Hive는 근본적으로 DW(DataWarehouse)를 구축하기 위한 목적으로 만들어 졌으며, SQL과 비슷한 HiveQL을 입력하면 MapReduce 방식으로 코드를 생성하여 HDFS의 파일을 처리한다.
>MapReduce
빅데이터 분산처리 시스템의 핵심 기술로
Map단계에서는 흩어져 있는 key, value로 데이터를 묶어주고
Reduce 단계에서는 Map단계의 key를 중심으로 필터링 및 정렬을 진행한다.


![hive1](https://user-images.githubusercontent.com/82218035/116034478-4b1a7200-a69e-11eb-99ce-98f9dde0bce6.PNG)



이처럼 Hive의 가장 큰 특징은 SQL이 MapReduce 프로그램으로 변환되어 HDFS의 DataNode에서 분산 실행된다는 것이다. 덕분에 SQL을 통한 Hadoop 데이터에 접근이 가능하고 분산 처리를 통해 빠른 처리가 가능해진다.
하지만 HiveQL은 분산 처리를 하는 관계로 ANSI-SQL을 모두 지원하지 않는다. ANSI-SQL을 모두 지원하지 않으므로 복잡한 분석 업무를 구현하기 위해서 QL이 매우 복잡해지는 단점이 있다.


Hive는 SQL을 이용하므로 DB, Table과 HDFS의 Path(디렉토리 경로)를 매핑하는 MetaData를 MetaStore라고 부르는 MetaData 저장소를 통해 관리한다. MetaStore는 Hive에서 가장 중요한 역할을 하는데 HiveDW에서 정의한 DB, Table, Partition 등을 모두 MetaStore에서 저장 및 관리하고 있고 HiveQL이 작동하면 MetaStore를 참고해 Hive의 런타임 환경이 만들지기 때문이다.


![hive2](https://user-images.githubusercontent.com/82218035/116034515-5ec5d880-a69e-11eb-9e9e-24807f276e04.PNG)


결론, 정리
- Hive는 MapReduce를 통한 데이터 탐색의 어려움을 극복하고자 개발한 빅데이터 탐색, 분석 도구이다.
- Hadoop의 HDFS에 저장되어 있는 파일과 Hbase에 적재되어있는 데이터를 SQL로 분석하고 처리하기 위한 환경을 제공한다.
- Hive의 MetaStore는 HiveDW의 DB, Table과 HDFS의 Path의 매핑정보를 관리하는 MetaData저장소이다.

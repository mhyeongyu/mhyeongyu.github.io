HDFS
==========

<br>

Hadoop(하둡)은 여러대의 컴퓨터를 하나로 묶어 대용량 데이터를 처리하는 기술로 빅데이터를 다루는 가장 대표적인 플랫폼이다. 하둡은 대용량 파일을 저장하는 HDFS와 저장된 파일을 빠르게 분산 처리하는 MapReduce(맵리듀스)로 구성되어 있으며, 빅데이터 플랫폼의 전체적인 생태계를 담당하고 있다. 빅데이터 플랫폼에서 데이터를 저장하는 Storage역할의 HDFS에 대해 알아보자.

![hdfs1](https://user-images.githubusercontent.com/82218035/116638699-d434f000-a9a1-11eb-9e26-bc94819643c8.PNG)

HDFS, Hadoop Distributed File System으로 빅데이터 기술의 핵심인 분산처리를 파일시스템에 적용하여 대용량의 파일을 보다 효율적으로 분산된 서버에 저장하고 처리하는 파일시스템이다. HDFS는 스트리밍 방식의 데이터 접근으로 대용량 데이터를 순차적으로 처리하기 때문에 원하는 부분의 데이터를 읽는 데 걸리는 지연 시간보다 전체 데이터를 모두 읽을 때 걸리는 시간을 더 중요시한다. 이러한 특징 때문에 HDFS는 빠른 응답 시간을 요구하는 작업이 아닌 빅데이터를 효율적으로 저장하는 저장소의 역할로 컴퓨터의 하드웨어와 비슷하다고 생각한다.

>파일시스템, 컴퓨터에서 파일을 쉽게 관리하도록 만든 체계이면서, 파일을 일정한 블록들의 배열로 분할하여 접근가능하도록 만든 시스템이다.

<br>

HDFS는 파일을 블록 단위로 나누고 저장한다. 일반적으로 블록은 디스크의 구역을 분할하여 사용하는 단위로 블록의 크기는 한 번에 읽고 쓸 수 있는 데이터의 최대량으로 설정된다. 보통 파일시스템에서 블록의 크기는 KB단위지만, HDFS은 탐색 비용을 최소화하기 위해 블록의 기본 크기를 128MB로 굉장히 큰 단위이다. 블록이 크면 각 블록의 시작점을 탐색하는 과정이 줄어들어 데이터의 전송에 더 집중할수있으므로 대용량 데이터 저장에 유리하기 때문이다. 그리고 HDFS의 블록은 일반적인 블록과 다르게 고정적인 크기가 아닌 저장된 파일에 따라 유연하게 크기를 변경하며 디스크를 사용한다.
![hdfs2](https://user-images.githubusercontent.com/82218035/116640145-20cdfa80-a9a5-11eb-8d96-9b657b655373.PNG)

<br>

HDFS는 MetaData(메타데이터)를 저장하고 있는 NameNode(네임노드)와 파일의 분할된 블록을 저장하고 있는 DataNode(데이터노드)로 이루어져 있으며, 파일 저장방식과 복구방식은 다음의 과정으로 진행된다.

- 파일 저장방식
  - 파일을 블록 단위로 분할하고 같은 파일의 블록들은 서로 다른 위치에 저장한다.
  - 각 파일의 블록은 3개의 복사본을 서로 다른 데이터노드에 분산시켜 저장한다.
  - 네임노드의 역할을 하는 노드는 블록과 복사본의 정보를 메타데이터로 관리한다.

![3](https://user-images.githubusercontent.com/82218035/115841774-19b06500-a458-11eb-8f1c-ae310f582cb0.PNG)

- 파일 복구방식
  - 네임노드의 메타데이터 정보를 통해 복구하고자 하는 파일의 블록과 저장되어 있는 데이터노드 위치를 파악한다.
  - 블록이 저장된 데이터노드 중 성능이 좋은 저장소를 파악하여 복구하고자 하는 블록의 위치 반환한다.
  - 데이터노드에서 반환받은 블록의 위치 정보로 블록을 찾고 합쳐서 파일을 복원한다.

![image3](https://user-images.githubusercontent.com/82218035/115553111-ff577980-a2e7-11eb-875d-e5113868ba4a.PNG)

<br>

###### 결론
- HDFS는 빅데이터 플랫폼인 Hadoop의 데이터 저장소인 Storage 역할을 하는 파일시스템이다.
- 일반적인 블록보다 큰 단위의 블록을 사용하여 빅데이터를 효율적으로 저장하고 처리한다.
- 네임노드와 데이터노드에 파일의 정보와 저장 위치를 기록하고 관리한다.

<!--
```
$hdfs dfs
$hdfs dfs -ls /
$hdfs dfs -mkdir /#NameNode

$hdfs dfs -put /#dir/#file /#NameNode
$hdfs dfs -rmr /#NameNode/#DataNode/#file

$hdfs dfs -cat /#NameNode/#DataNode/#file
#hdfs dfs -get /#NameNode/#DataNode/#file /#dir/#file
```-->

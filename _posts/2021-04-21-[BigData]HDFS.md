HDFS
========================================

<br>

- 하둡 프레임워크를 위해 java언어로 만들어진 **분산 확장 파일 시스템이다.** <br>
- 대용량 파일을 분산된 서버에 저장하고 클라이언트가 데이터를 빠르게 처리 가능하도록 해준다. <br>  
- 간략히 말하면 **HDFS는 대용량 데이터를 저장, 배치하고 처리하기위한 파일 시스템이다.** <br>  
- HDFS는 크게 MetaData를 저장하고 있는 **NameNode**와 파일의 분할된 Block들을 저장하고 있는 **DataNode**로 이루어져 있다. <br>

<br>



HDFS 저장방식
--------------------

![1](https://user-images.githubusercontent.com/82218035/115841674-ff768700-a457-11eb-80cf-93d16609b819.PNG){: width="400px", height="300px"}
![2](https://user-images.githubusercontent.com/82218035/115841740-11f0c080-a458-11eb-80ec-1fc6b05d85ee.PNG){: width="400px", height="300px"}
![3](https://user-images.githubusercontent.com/82218035/115841774-19b06500-a458-11eb-8f1c-ae310f582cb0.PNG){: width="400px", height="300px"}


1. 저장하고자 하는 파일을 **Block 단위로 분할**하고 같은 파일의 Block들은 서로 다른 위치에 저장한다.
2. 각 파일의 Block은 Block마다 3개의 복사본을 서로 다른 **Data Node에 분산시켜 저장한다.**
3. Name Node의 역할을 하는 컴퓨터는 Block과 복사본의 정보를 **meta data로 관리한다.**

<br>

HDFS 복구방식
--------------------

![image1](https://user-images.githubusercontent.com/82218035/115553106-fd8db600-a2e7-11eb-859c-929d1634084f.PNG){: width="400px", height="300px"}
![image2](https://user-images.githubusercontent.com/82218035/115553110-febee300-a2e7-11eb-91c5-c475dcc4b1a0.PNG){: width="400px", height="300px"}
![image3](https://user-images.githubusercontent.com/82218035/115553111-ff577980-a2e7-11eb-875d-e5113868ba4a.PNG){: width="400px", height="300px"}


1. Name Node의 MetaData 정보를 통해 복구하고자 하는 파일의 Block과 저장되어 있는 Data Node 위치를 파악한다.
2. Block이 저장된 Data Node 중 성능이 좋은 저장소를 파악하여 복구하고자 하는 Block의 위치 반환한다.
3. Data Node에서 반환받은 Block의 위치를 통해 Block을 찾고 합쳐서 파일을 복원한다.


<br>


```
$hdfs dfs
$hdfs dfs -ls /
$hdfs dfs -mkdir /#NameNode

$hdfs dfs -put /#dir/#file /#NameNode
$hdfs dfs -rmr /#NameNode/#DataNode/#file

$hdfs dfs -cat /#NameNode/#DataNode/#file
#hdfs dfs -get /#NameNode/#DataNode/#file /#dir/#file
```
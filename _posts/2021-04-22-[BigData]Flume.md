Flume
===============
Flume은 로그 데이터 수집을 위해 개발한 **빅데이터 수집 소프트웨어**로 스트리밍 데이터인 로그 데이터를 병렬적으로 분산처리하면서 수집한다.

![2](https://user-images.githubusercontent.com/82218035/115861329-a3b6f880-a46d-11eb-98e3-6ed5b3909514.PNG)


Flume 수집방식
----------------
Flume은 디렉토리 감시를 통해 업로드되는 데이터를 수집하는 방식으로
1. Source에서 해당 파일을 읽고 데이터를 Channel로 전달한다.
2. Channel은 Source와 Sink를 연결하고 데이터의 흐름을 제어하는 버퍼링 역할을 한다.
3. Sink는 Channel에서 전달받은 데이터를 최종 목적지인 HDFS, HBase로 저장한다.

<br>

Flume 구성요소
------------------
![image1](https://user-images.githubusercontent.com/82218035/115861404-b6313200-a46d-11eb-936c-72725954cfe1.PNG)
- Source : 새로운 파일 업로드 **감시**, 새로운 파일 Channel로 전달
- Channel : Source와 Sink를 연결, 읽어 온 데이터 **임시저장**
- Sink : 최종적으로 데이터를 목적지에 **저장**

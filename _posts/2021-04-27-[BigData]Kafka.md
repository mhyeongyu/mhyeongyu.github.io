kafka
===================

<br>

오늘날 실시간으로 발생하는 로그 데이터의 양이 방대해지고, BigData가 생겨나면서 실시간으로 대량의 데이터를 취급하기 위한 시스템이 필요해졌다. 이를 해결하기 위해 2011년 링크드인에서 웹사이트에서 생성되는 많은 양의 로그를 처리하기 위한 목적으로 Kafka를 개발했다.


![kafka3](https://user-images.githubusercontent.com/82218035/116209670-1a5d3a00-a77d-11eb-8900-39111d65465b.PNG)


Kafka는 대규모로 발생하는 메시지성, StreamingData를 비동기 방식으로 중계하는 역할을 한다. 대규모 트랜잭션 데이터가 발생했을때 데이터 전송시 중간에 데이터를 버퍼링하며, 전달하고자 하는 시스템에 안정적으로 데이터를 전송해준다. 만약 Flume이 수집한 데이터를 Kafka를 거치지 않고 곧바로 HBase로 전송시 HBase에 장애가 발생하면 Flume의 Channel에 전송하지 못한 데이터들이 쌓여 Flume에서 2차적인 장애가 발생한다. 그리고 실시간 발생하는 데이터 수집이 불가능해 데이터 유실이 발생한다. 이렇듯 kafka는 수집한 실시간 데이터를 안정적으로 적재시키기 위해 중간의 파이프라인 같은 역할을 한다.

>비동기방식
작업이 끝나지 않더라도 나머지 작업을 먼저 실행한다.
분산 처리 방식과 비슷한 개념이라 보인다.

<br>

Kafka의 구성요소로 Broker, Topic, Provider, Consumer 가 있다. Broker는 Kafka의 인스턴스로 Producer와 Consumer사이에 위치하며, Topic이 생성되는 물리적인 서버이다. Topic은 Kafka의 유사한 메시지들을 저장하는 저장소로 창고의 역할을 한다. Provider는 메시지를 전송하는 역할을 하고 반대로 Consumer는 메시지를 수신하는 역할을 한다.


![kafka1](https://user-images.githubusercontent.com/82218035/116209732-28ab5600-a77d-11eb-84a4-410fc1a9481c.PNG)


Kafka의 Broker에 메시지를 저장할 Topic을 생성하고 Broker는 Topic을 기준으로 메시지를 관리한다. Producer는 Topic의 메시지를 생성한 뒤 Broker에게 전달하고 Broker는 전달받은 메시지를 Topic에 맞춰 분류하면, 각자의 Topic을 담당하는 Consumer들이 메시지를 가져와 처리한다.

<br>

결론
- Kafka는 대규모로 발생하는 메시지성, StreamingData를 비동기 방식으로 중계하는 역할을 한다.
- Flume에서 수집한 데이터를 다음 시스템에 안정적으로 전달해준다.
- Broker-Topic-Consumer 순서로 메시지를 처리한다.

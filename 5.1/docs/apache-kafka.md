# Apache Kafka

[Kafka](http://kafka.apache.org) 는 분산 메시징시스템으로, 발행-구독(publish-subscribe) 모델을 기반으로 동작하며 producer, consumer, broker로 구성됩니다. 

## 설치

[download](http://kafka.apache.org/downloads) 페이지에서 다운받습니다(ex. `kafka_2.12-2.1.0.tgz`). 

```bash
$ tar -xzf ~/Downloads/kafka_2.12-2.1.0.tgz -C ~/Desktop/   # Desktop폴더에 압축풀기
$ cd ~/Desktop/kafka_2.12-2.1.0/                            # 설치폴더로 이동 
$ bin/zookeeper-server-start.sh config/zookeeper.properties # zookepper 실행
$ bin/kafka-server-start.sh config/server.properties        # kafka 실행
```
## Kafka Tool

[download](http://www.kafkatool.com/download.html) 페이지에서 Kafka UI Tool 를 다운받을 수 있습니다(ex. `kafkatool.exe`).  


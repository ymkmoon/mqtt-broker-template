# mqtt-broker-template

EMQX 클러스터 (MQTT Broker)

카프카 설치 및 테스트 명령어

MQTT Publisher -> **EMQX 클러스터 (MQTT Broker)** -> Kafka Broker -> Consumer

- MQTT Publisher : 추가예정
- MQTT Broker : https://github.com/ymkmoon/kafka-broker-template
- Kafka Broker : https://github.com/ymkmoon/kafka-broker-template
- Consumer : https://github.com/ymkmoon/springboot-consumer-template

## 빌드

### 1. EMQX 이미지 빌드 및 컨테이너 실행 

```bash
# 로컬 환경
docker compose -p emqx-cluster --env-file emqx.local.env up -d

# 개발 환경
docker compose -p emqx-cluster --env-file emqx.dev.env up -d
```

## ETC

- 네트워크 공유
  - EMQX 와 Kafka 는 별도 Compose 이기 때문에 Docker 네트워크 공유

```bash
# 네트워크 생성
docker network create iot-net

# Kafka Compose
docker compose -p kafka-cluster --env-file kafka.env up -d
# EMQX Compose
docker compose -p emqx-cluster --env-file emqx.env up -d

# 두 Compose 모두 iot-net 네트워크에 연결
docker network connect iot-net kafka1
docker network connect iot-net kafka2
docker network connect iot-net kafka3

docker network connect iot-net emqx1
docker network connect iot-net emqx2
docker network connect iot-net emqx3
```
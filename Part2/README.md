## Note
Please complete Part1 before starting Part2

# Installation with Docker

We might come across an error with "*wurstmeister*" image.

```
'image's platform (linux/amd64) does not match the detected host platform (linux/arm64/v8)'
```

### Workaround: 

Try adding this while building the docker images,

```
--platform linux/amd64
```

#### However, it is better to avoid it altogether.

Unfortunately, "*wurstmeister*" doesn't have a zookeeper image for arm. We can switch to "*bitnami*" instead.

```
services:
  zookeeper:
    image: docker.io/bitnami/zookeeper
    container_name: zookeeper
    ports:
      - "2181:2181"
    environment:
      ALLOW_ANONYMOUS_LOGIN: yes
  kafka:
    image: docker.io/bitnami/kafka
    container_name: kafka
    ports:
      - "9092:9092"
    environment:
      KAFKA_ADVERTISED_HOST_NAME: localhost
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
```


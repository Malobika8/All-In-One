# End-to-End Integration Testing in Spring Boot with Test containers

Without integration testing, we cannot be confident about the stability of our production environment.

We can use TestContainer which can reduce test configuration to almost zero.

Close Zookeeper and Kafka esrver. We want don't want to use these. Rather we will be taking the help of TestContainers to spin up a new Kafka instance for us.


Add dependencies:

```
<!-- https://mvnrepository.com/artifact/org.testcontainers/testcontainers -->
<dependency>
    <groupId>org.testcontainers</groupId>
    <artifactId>testcontainers</artifactId>
    <version>1.20.1</version>
    <scope>test</scope>
</dependency>
<!-- https://mvnrepository.com/artifact/org.testcontainers/kafka -->
<dependency>
    <groupId>org.testcontainers</groupId>
    <artifactId>kafka</artifactId>
    <version>1.20.1</version>
    <scope>test</scope>
</dependency>
<!-- https://mvnrepository.com/artifact/org.testcontainers/junit-jupiter -->
<dependency>
    <groupId>org.testcontainers</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>1.20.1</version>
    <scope>test</scope>
</dependency>
```

Add this dependency to wait for some time while running the producer & consumer. It's a utility package.

```
<!-- https://mvnrepository.com/artifact/org.awaitility/awaitility -->
		<dependency>
			<groupId>org.awaitility</groupId>
			<artifactId>awaitility</artifactId>
			<version>4.2.0</version>
			<scope>test</scope>
		</dependency>
```

## Producer Application

- Create a test class.
- We want to run the tests in a random port.

  <img width="894" alt="Screenshot 2024-08-29 at 1 44 54 PM" src="https://github.com/user-attachments/assets/9756a311-4328-414f-92e2-ee1a7c168b5a">

- We need to tell SpringBoot that the test class uses test containers.

  <img width="945" alt="Screenshot 2024-08-29 at 1 45 02 PM" src="https://github.com/user-attachments/assets/da78aef0-9c42-468b-907a-6ecb1391946f">

- Create Kafka container: We want to use the Kafka container. We can check out this documentation to create a Kafka container.

  https://java.testcontainers.org/modules/kafka/
  
  This will get us the latest Kafka container or the one(version) that we have specified.

  ```
  KafkaContainer kafka = new KafkaContainer(DockerImageName.parse("confluentinc/cp-kafka:6.2.1"))
  ```

  <img width="1071" alt="Screenshot 2024-08-29 at 1 45 19 PM" src="https://github.com/user-attachments/assets/d01e3f29-848f-4bb1-a5eb-61b8193d33c6">

- Configure the bootstrap server.

  <img width="1082" alt="Screenshot 2024-08-29 at 1 45 29 PM" src="https://github.com/user-attachments/assets/504f05f8-8132-47cd-a090-be063d68ea0a">

- Write the actual test

  <img width="1063" alt="Screenshot 2024-08-29 at 1 45 36 PM" src="https://github.com/user-attachments/assets/76ac6155-24e2-42be-892b-98ac6116859a">

- Add application.yml to the test/resources folder. We need to remove the bootstrap server as it will be provided by the kafka container      and the port generated will be random.

  <img width="1307" alt="Screenshot 2024-08-29 at 1 48 53 PM" src="https://github.com/user-attachments/assets/f585d65c-5851-4e05-bf44-e0753831a3d9">

- Run the test. Make sure Docker is running.

  <img width="1064" alt="Screenshot 2024-08-29 at 1 43 40 PM" src="https://github.com/user-attachments/assets/cecc8c67-77ed-444f-9aee-9a4cc661d874">
  <img width="1076" alt="Screenshot 2024-08-29 at 1 43 51 PM" src="https://github.com/user-attachments/assets/fe08b43f-6b4b-4a58-a434-7e20358a437d">

```
package com.kafka.producer_example;

import com.kafka.producer_example.dto.Customer;
import com.kafka.producer_example.service.KafkaMessagePublisher;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.DynamicPropertyRegistry;
import org.springframework.test.context.DynamicPropertySource;
import org.testcontainers.containers.KafkaContainer;
import org.testcontainers.junit.jupiter.Container;
import org.testcontainers.junit.jupiter.Testcontainers;
import org.testcontainers.utility.DockerImageName;

import java.time.Duration;
import java.util.concurrent.TimeUnit;

import static org.awaitility.Awaitility.await;

@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
@Testcontainers
class ProducerExampleApplicationTests {

	@Container
	static KafkaContainer kafka = new KafkaContainer(DockerImageName.parse("confluentinc/cp-kafka:latest"));

	@DynamicPropertySource
	public static void initKafkaProperties(DynamicPropertyRegistry registry){
		registry.add("spring.kafka.bootstrap-servers",kafka::getBootstrapServers);
	}

	@Autowired
	private KafkaMessagePublisher publisher;

	@Test
	public void testSendEventToTopic(){
		publisher.sendEventToTopic(new Customer(1,"test","test@gmail.com","1234567"));
		await().pollInterval(Duration.ofSeconds(3)).atMost(10, TimeUnit.SECONDS).untilAsserted(()->{

		});
	}

}
```

## Consumer Application

- Create a test class.
- We want to run the tests in a random port.
- We need to tell SpringBoot that the test class uses test containers.
- Create Kafka container: We want to use the Kafka container. We can check out this documentation to create a Kafka container.

  https://java.testcontainers.org/modules/kafka/
  
  This will get us the latest Kafka container or the one(version) that we have specified.

  ```
  KafkaContainer kafka = new KafkaContainer(DockerImageName.parse("confluentinc/cp-kafka:6.2.1"))
  ```
- Configure the bootstrap server.
- Write the actual test

  <img width="1015" alt="Screenshot 2024-08-29 at 2 34 16 PM" src="https://github.com/user-attachments/assets/f740b6d9-a3ec-4a7e-be33-99f4e4e1b1ec">

- Add application.yml to the test/resources folder. We need to remove the bootstrap server as it will be provided by the kafka container      and the port generated will be random.

  <img width="984" alt="Screenshot 2024-08-29 at 2 35 31 PM" src="https://github.com/user-attachments/assets/654b9a17-9a1a-4bf7-957f-4ac0d5a0594e">

- Run the test. Make sure Docker is running.

```
package com.kafka.consumer_example;

import com.kafka.consumer_example.dto.Customer;
import lombok.extern.slf4j.Slf4j;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.kafka.core.KafkaTemplate;
import org.springframework.test.context.DynamicPropertyRegistry;
import org.springframework.test.context.DynamicPropertySource;
import org.testcontainers.containers.KafkaContainer;
import org.testcontainers.junit.jupiter.Container;
import org.testcontainers.junit.jupiter.Testcontainers;
import org.testcontainers.utility.DockerImageName;

import java.time.Duration;
import java.util.concurrent.TimeUnit;

import static org.awaitility.Awaitility.await;

@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
@Testcontainers
@Slf4j
class ConsumerExampleApplicationTests {

	@Container
	static KafkaContainer kafka = new KafkaContainer(DockerImageName.parse("confluentinc/cp-kafka:latest"));

	@DynamicPropertySource
	public static void initKafkaProperties(DynamicPropertyRegistry registry){
		registry.add("spring.kafka.bootstrap-servers",kafka::getBootstrapServers);
	}

	@Autowired
	KafkaTemplate<String, Object> kafkaTemplate;

	@Test
	public void testConsume1(){
		log.info("test execution started..");
		kafkaTemplate.send("demo-topic", new Customer(1,"test","test@gmail.com","1234567"));
		log.info("test execution ended");
		await().pollInterval(Duration.ofSeconds(3)).atMost(10, TimeUnit.SECONDS).untilAsserted(()->{

		});
	}

}
```




  



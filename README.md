# Project Overview

This project is a microservices-based application built with Java, Spring Boot, and Apache Kafka. It includes a service that ingests data from Twitter and publishes it to a Kafka cluster for further processing.

## Components

### 1. twitter-to-kafka-service
- **Description:**  
  A Spring Boot microservice that connects to the Twitter API, streams tweets based on configured criteria, and publishes them to a Kafka topic.
- **Configuration:**  
  - Requires valid Twitter API credentials in the `twitter4j.properties` file.
  - Kafka connection details are configured in the application's `application.yml` or `application.properties`.

### 2. Kafka Cluster
- **Description:**  
  A multi-node Kafka cluster managed via Docker Compose, used for message brokering between microservices.
- **Configuration:**  
  - Defined in the `docker-compose/services.yml` file.
  - Includes Zookeeper and Kafka broker services.

### 3. Docker Compose
- **Description:**  
  Orchestrates the deployment of the Kafka cluster and the `twitter-to-kafka-service` microservice.
- **Configuration:**  
  - All service definitions are in the `docker-compose/services.yml` file.
  - Ensures all dependencies are started in the correct order.

## Prerequisites

- Java 17 or higher
- Maven 3.6+
- Docker and Docker Compose
- Twitter API credentials

## Setup Instructions

1. **Configure Twitter Credentials**
   - Edit the `twitter4j.properties` file and enter your Twitter API credentials.

2. **Build the Application**
   - Run the following command to build the project and create a Docker image (tests are skipped for faster build):
     ```
     mvn install -DskipTests
     ```
   - The `spring-boot-maven-plugin` in `pom.xml` is configured to build a Docker image during the Maven build.

3. **Start the Kafka Cluster and Microservice**
   - Navigate to the `docker-compose` directory:
     ```
     cd docker-compose
     ```
   - Start all services using Docker Compose:
     ```
     docker-compose up
     ```

4. **Verify the Setup**
   - The `twitter-to-kafka-service` should start and begin streaming tweets to the Kafka topic.
   - Kafka and Zookeeper containers should be running and accessible.

## File Structure

- `twitter4j.properties` — Twitter API credentials.
- `pom.xml` — Maven build configuration, including Docker image build setup.
- `docker-compose/services.yml` — Docker Compose definitions for Kafka, Zookeeper, and microservices.
- `src/main/resources/application.yml` — Spring Boot application configuration.

## Additional Notes

- You can customize the tweet filtering criteria in the `twitter-to-kafka-service` configuration.
- Logs and error messages are available in the respective Docker container logs.
- For development, you can run the Spring Boot service locally and connect to the Dockerized Kafka cluster.

## Troubleshooting

- Ensure Docker and Docker Compose are installed and running.
- Check that the Twitter API credentials are correct and have the necessary permissions.
- If the Kafka service is not reachable, verify the network settings in `services.yml`.

## License

This project is licensed under the MIT License.# Running the application
- Please enter the correct credentials in twitter4j.properties file.
- Then run mvn install -DskipTests command
- Then go to docker-compose folder and run docker-compose up command to run kafka cluster and twitter-to-kafka-service together
- Check the pom.xml file and spring-boot-maven-plugin section in twitter-to-kafka-service, where we configure 
the build-image goal to create docker image with mvn install command
- Check the services.yml file under docker-compose folder which includes the compose definition 
for microservice, twitter-to-kafka-service
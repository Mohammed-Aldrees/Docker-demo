
# Spring Boot Application Dockerization

This repository contains the necessary files to containerize and deploy a Java Spring Boot application using Docker.

## Prerequisites

To build and run the Docker image, ensure that you have the following prerequisites installed on your local machine:

- Docker: You can download and install Docker from the official website: [https://www.docker.com](https://www.docker.com)

## Usage

Follow the steps below to build and run the Docker image for the Spring Boot application:

1. Clone this repository to your local machine:

   ```shell
   git clone https://github.com/mohammad767/java-docker.git
   cd java-docker
   ```

2. Build the Docker image by executing the following command:

   ```shell
   docker build -t java-docker .
   ```

   This command uses the Dockerfile in the repository to build an image with the tag `spring-boot-app`.

3. Run the Docker container based on the image you just built:

   ```shell
   docker run -p 8080:8080 java-docker
   ```

   The application will be accessible at `http://localhost:8080`.

## Dockerfile Details

The Dockerfile in this repository has the following structure:

```dockerfile
FROM eclipse-temurin:17-jdk-jammy

WORKDIR /app

COPY .mvn/ .mvn
COPY mvnw pom.xml ./
RUN ./mvnw dependency:resolve

COPY src ./src

CMD ["./mvnw", "spring-boot:run"]
```

The Dockerfile starts with the base image `eclipse-temurin:17-jdk-jammy`, which provides the Java Development Kit (JDK) version 17.

- The `WORKDIR /app` instruction sets the working directory within the Docker image to `/app`.

- The `COPY` instructions copy the Maven wrapper files (`mvnw` and `.mvn/`) and the `pom.xml` file into the image's `/app` directory.

- The `RUN ./mvnw dependency:resolve` command resolves the project dependencies using Maven.

- The `COPY src ./src` instruction copies the application source code from the local file system into the `/app/src` directory within the Docker image.

- Finally, the `CMD` instruction specifies the command to run when the Docker container starts. It executes the Spring Boot application using the Maven wrapper.

Feel free to modify the Dockerfile and adapt it to your specific requirements.


FROM maven:3.8.5-openjdk-17-slim@sha256:5ba3fae0f77cbe08deac4984dfa4f5397345d5ba8221871285a96e2ef8f16808 AS builder

MAINTAINER sdnv

ADD ./pom.xml pom.xml
ADD ./src src/
RUN mvn clean package

FROM openjdk:22-ea-17-jdk-slim-bullseye@sha256:b9785c8c9bd6878684ad2302c704b5a60444ffb7c58fb75276ff54bfbbf5a59e

RUN apt update && \
    apt install dumb-init -y

WORKDIR /opt/app

COPY --from=builder target/hellodocker-0.0.1-SNAPSHOT.jar hellodocker.jar

RUN useradd --shell /bin/false appuser && \
    chown -R appuser:appuser /opt/app

USER appuser

EXPOSE 8080

ENTRYPOINT ["dumb-init", "java", "-jar", "hellodocker.jar"]

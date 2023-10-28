FROM maven:3.8.5-openjdk-17-slim AS builder

MAINTAINER sdnv

ADD ./pom.xml pom.xml
ADD ./src src/
RUN mvn clean package

FROM openjdk:22-ea-17-jdk-slim-bullseye

RUN apt update && \
    apt install dumb-init -y

WORKDIR /opt/app

COPY --from=builder target/hellodocker-0.0.1-SNAPSHOT.jar hellodocker.jar

RUN useradd --shell /bin/false appuser && \
    chown -R appuser:appuser /opt/app

USER appuser

EXPOSE 8080

ENTRYPOINT ["dumb-init", "java", "-jar", "hellodocker.jar"]

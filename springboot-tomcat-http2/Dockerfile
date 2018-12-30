# https://docs.spring.io/spring-boot/docs/current/reference/html/howto-embedded-web-servers.html
FROM openjdk:8u171-jdk-alpine AS builder

RUN apk add --no-cache git

RUN git clone https://github.com/heowc/spring-boot-jenkins.git && \
    cd spring-boot-jenkins && \
    ./gradlew clean build -x test

FROM openjdk:8u171-jre-alpine

RUN apk add --no-cache tomcat-native

COPY --from=builder /spring-boot-jenkins/build/libs/spring-boot-jenkins-0.0.1-SNAPSHOT.jar /home/docker/app.jar
COPY sample.jks /home/docker

ENTRYPOINT java -jar \
            -Djava.library.path=/usr/lib \
            -Dserver.http2.enabled=true \
            -Dserver.port=8443 \
            -Dserver.ssl.key-store=/home/docker/sample.jks \
            -Dserver.ssl.key-store-password=secret \
            -Dserver.ssl.key-password=password \
            /home/docker/app.jar
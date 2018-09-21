FROM maven:3.5.4-jdk-8-alpine as build
 
RUN apk update \
    && apk upgrade \
    && apk add --no-cache bash git openssh
 
RUN git clone https://github.com/heowc/cafe24-exam-timetable.git \
    && cd cafe24-exam-timetable \
    && mvn clean package
 
FROM openjdk:8u171-jre-alpine
 
COPY --from=build /cafe24-exam-timetable/target/cafe24-exam-timetable-0.0.1-SNAPSHOT.jar app.jar
 
EXPOSE 8080
 
ENTRYPOINT ["java", "-jar", "app.jar"]

FROM maven:3.5.2-alpine as builder
WORKDIR /usr/src/app
COPY pom.xml .
RUN mvn compile
COPY src /usr/src/app/src
RUN mvn package
FROM openjdk:alpine
ENV HOST='0.0.0.0'
ENV PORT='8080'
EXPOSE $PORT
WORKDIR /usr/src/app
COPY --from=builder /usr/src/app/target/casestudy-0.0.1-SNAPSHOT.jar .
CMD java -jar -Dspring.profiles.active=docker casestudy-0.0.1-SNAPSHOT.jar

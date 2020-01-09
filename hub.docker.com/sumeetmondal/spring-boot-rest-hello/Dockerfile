FROM maven:3.5-jdk-8-alpine as build
COPY ./pom.xml ./pom.xml
RUN mvn dependency:go-offline -B
COPY ./src ./src
RUN mvn clean install

FROM openjdk:8-jdk-alpine
EXPOSE 8763
COPY --from=build /dist/spring-boot-rest-hello-0.0.1-SNAPSHOT.jar ./spring-boot-rest-hello.jar
ENTRYPOINT ["java","-jar","./spring-boot-rest-hello.jar"]
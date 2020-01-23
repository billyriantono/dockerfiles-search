FROM maven:3.5-jdk-8 AS build
MAINTAINER Shubham Kumar <subhamsahu2010@gmail.com>
COPY src /usr/src/app/src
COPY pom.xml /usr/src/app
RUN mvn -f /usr/src/app/pom.xml clean package
FROM gcr.io/distroless/java
COPY --from=build /usr/src/app/target/eureka-server-1.0.0.jar /usr/app/eureka-server-1.0.0.jar
EXPOSE 8001
ENTRYPOINT ["java","-jar","/usr/app/eureka-server-1.0.0.jar"]
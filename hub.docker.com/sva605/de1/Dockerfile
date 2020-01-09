FROM maven:latest as builder
RUN apt update && apt install git
RUN git clone https://github.com/sva605/docker-example && cd docker-example && mvn clean package

FROM openjdk:8-alpine
COPY --from=builder /docker-example/target/docker-example.jar docker-example.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","docker-example.jar"]


#FROM openjdk:8-jre-alpine
#EXPOSE 8080
#COPY /target/docker-example.jar docker-example.jar
#ENTRYPOINT ["java"]
#CMD ["-jar","-Djava.security.egd=file:/dev/./urandom","/docker-example.jar"]


#FROM maven:3.6.2-jdk-8 as builder
#WORKDIR /tmp/
#COPY pom.xml /tmp/
#COPY src /tmp/src/
#RUN mvn package
#
#FROM openjdk:8-jre-alpine
#COPY --from=builder /tmp/target/docker-example.jar docker-example.jar
#EXPOSE 8080
#ENTRYPOINT ["java"]
#CMD ["-jar","-Djava.security.egd=file:/dev/./urandom","/docker-example.jar"]

FROM maven:3.6.2-slim as builder
COPY /demaPersistence/. /usr/app 
WORKDIR /usr/app
RUN mvn install

FROM openjdk:8 
MAINTAINER Filippo Giuffrida
COPY --from=builder /usr/app/target/demapersistence.jar /usr/app/demapersistence.jar

EXPOSE 8082 
ENTRYPOINT ["java", "-jar", "/usr/app/demapersistence.jar"]





FROM maven:3.6.2-slim as builder
COPY . /usr/app 
WORKDIR /usr/app
RUN mvn install

FROM openjdk:8 
MAINTAINER Filippo Giuffrida
COPY --from=builder /usr/app/target/urlshortener.jar /usr/app/urlshortener.jar

EXPOSE 8086 
ENTRYPOINT ["java", "-jar", "/usr/app/urlshortener.jar"]





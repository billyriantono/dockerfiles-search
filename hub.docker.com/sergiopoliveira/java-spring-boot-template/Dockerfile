FROM maven:3.6.1-jdk-11

COPY . /usr/app/

WORKDIR /usr/app

RUN mvn package

EXPOSE 8080

CMD ["java", "-jar", "target/java-spring-boot-template-0.0.1-SNAPSHOT.jar"]
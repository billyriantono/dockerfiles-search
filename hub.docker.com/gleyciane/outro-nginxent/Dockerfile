FROM maven:3.5-jdk-8 AS build
COPY src /usr/glarimy/src
COPY pom.xml /usr/glarimy
RUN mvn -f /usr/glarimy/pom.xml clean package
EXPOSE 9000
ENTRYPOINT ["java", "-jar","/usr/glarimy/target/glarimy-employee-service-1.0.0.jar"]
FROM openjdk:8-jdk-alpine
COPY portfolio-1.0.0-SNAPSHOT.jar app.jar
ENTRYPOINT ["java","-jar","-Dspring.profiles.active=gcp","/app.jar"]

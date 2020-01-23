FROM openjdk:8-jdk-alpine
COPY target/search-0.0.1-SNAPSHOT.jar lookup.jar
EXPOSE 8123
CMD ["java","-jar","/lookup.jar"]

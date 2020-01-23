#Step: Package Maven Artifact
FROM maven:3.6.2-jdk-8 AS MAVEN_BUILD
COPY pom.xml /tmp
WORKDIR /tmp/
RUN mvn dependency:go-offline

COPY src /tmp/src/
RUN mvn package


#Step: Package Image
FROM openjdk:8-jdk-alpine
COPY --from=MAVEN_BUILD /tmp/target/edp-adapter-*.jar app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
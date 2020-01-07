FROM maven:3.5.2-jdk-8-alpine as CREATED_JAR
COPY pom.xml /tmp/
COPY src /tmp/src/
WORKDIR /tmp/
RUN mvn clean package -DskipTests

FROM openjdk:8-jre-alpine
COPY --from=CREATED_JAR /tmp/target/github-packages-poc.jar /tmp/github-packages-poc.jar
WORKDIR /tmp/
ENV JAVA_OPTS=""
ENTRYPOINT exec java $JAVA_OPTS -Djava.security.egd=file:/dev/./urandom -jar github-packages-poc.jar
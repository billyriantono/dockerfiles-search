FROM maven:3-jdk-10 as BUILD

COPY . /usr/src/app
RUN mvn --batch-mode -f /usr/src/app/pom.xml clean package

FROM openjdk:10-jre-slim
RUN apt-get update && \
    apt-get install -y git

COPY --from=BUILD /usr/src/app/updatebot/target/updatebot-1.1-SNAPSHOT.jar /opt/target/updatebot.jar
WORKDIR /opt/target

ENTRYPOINT [ "java", "-jar", "updatebot.jar" ]
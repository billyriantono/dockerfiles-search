FROM maven:3.5.2-jdk-8-alpine AS MAVEN_BUILD

MAINTAINER MiGuards

COPY ./ /build/
WORKDIR /build/
RUN mvn clean install && cd web-module && mvn clean install spring-boot:repackage && cd ..

FROM openjdk:8-jre-alpine
ARG profile_variable
VOLUME /tmp
WORKDIR /tmp
COPY --from=MAVEN_BUILD /build/web-module/target/web-module-1.0-SNAPSHOT.jar miguards-backend.jar
ENTRYPOINT exec java -jar -Dspring.profiles.active=${profile_variable} miguards-backend.jar

FROM openjdk:8-jdk-alpine as build
WORKDIR /workspace/app

#ADD VERSION ../.

COPY mvnw .
COPY .mvn .mvn
COPY pom.xml .
COPY src src

RUN ./mvnw install -DskipTests



FROM openjdk:8-jdk-alpine
VOLUME /tmp1

ARG DEPENDENCY=/workspace/app/target
COPY --from=build ${DEPENDENCY}/*jar /opt/app.jar
COPY src/main/resources/application.properties /opt/application.properties

CMD  java -jar /opt/app.jar

EXPOSE 8081


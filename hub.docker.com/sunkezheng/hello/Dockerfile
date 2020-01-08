FROM openjdk:11

WORKDIR /workspace/app

COPY mvnw .
COPY .mvn .mvn
COPY pom.xml .
COPY src src

RUN ./mvnw package -DskipTests

ENTRYPOINT ["java","-jar","target/hello-0.0.1-SNAPSHOT.jar"]
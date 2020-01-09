FROM maven AS builder
ARG build_command="mvn package -Dmaven.test.skip=true"
WORKDIR /app
COPY . .
RUN ${build_command}

FROM openjdk:8

COPY --from=builder /app/target/spring-petclinic-2.2.0.BUILD-SNAPSHOT.jar /app.jar

EXPOSE 8080

CMD java -jar /app.jar 

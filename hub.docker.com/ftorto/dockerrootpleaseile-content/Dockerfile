FROM maven:3.6.1-slim as builder
COPY pom.xml /app/pom.xml
WORKDIR /app
RUN mvn dependency:go-offline

COPY src /app/src
RUN mvn clean package

FROM adoptopenjdk/openjdk11:alpine-jre
COPY /jmx /app/jmx
COPY --from=builder /app/target/WorkloadSimulator-0.1.jar /app/WorkloadSimulator-0.1.jar
WORKDIR /app
EXPOSE 9088
ENTRYPOINT ["java","-javaagent:./jmx/jmx_prometheus_javaagent-0.12.0.jar=9088:./jmx/config-jmx.yaml", "-jar", "WorkloadSimulator-0.1.jar"]
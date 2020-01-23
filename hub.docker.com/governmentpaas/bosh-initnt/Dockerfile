FROM maven:3.6.1-jdk-8-slim
MAINTAINER "Mahendra"
WORKDIR /app
COPY src /app/src
COPY pom.xml /app/pom.xml
RUN mvn -f /app/pom.xml -s /usr/share/maven/ref/settings-docker.xml clean install
ENTRYPOINT exec java -jar /app/target/discovery.jar com.mgtechno.DiscoveryServiceApplication
EXPOSE 0.0.0.0:8761:8761

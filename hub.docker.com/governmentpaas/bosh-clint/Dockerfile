FROM maven:3.6.1-jdk-8-slim
MAINTAINER "Mahendra"
WORKDIR /app
COPY . /app/.
RUN mvn -f /app/pom.xml -s /usr/share/maven/ref/settings-docker.xml dependency:resolve clean install
ENTRYPOINT exec java -jar /app/target/customer.jar com.mgtechno.CustomerApplication
EXPOSE 0.0.0.0:8082:8082
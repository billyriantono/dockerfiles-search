FROM openjdk:8-jdk-alpine
VOLUME /config
VOLUME /tmp
EXPOSE 8888

LABEL maintainer="Brian Schalme <bschalme@airspeed.ca>"

COPY . /opt/spring-cloud-config-server/
WORKDIR /opt/spring-cloud-config-server/
RUN ./gradlew build && \
  cp ./build/libs/spring-cloud-config-server-*.jar /opt/spring-cloud-config-server.jar && \
  rm -rf /opt/spring-cloud-config-server/* && \
  rm -rf ~/.gradle/*

WORKDIR /opt
ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "-jar", "spring-cloud-config-server.jar"]

FROM openjdk:8-jdk-alpine
VOLUME /tmp
VOLUME /config
EXPOSE 8761

LABEL maintainer="Brian Schalme <bschalme@airspeed.ca>"

COPY . /opt/eureka-server/
WORKDIR /opt/eureka-server
RUN ./gradlew build && \
  cp ./build/libs/eureka-server-*.jar /opt/eureka-server.jar && \
  rm -rf /opt/eureka-server/* && \
  rm -rf ~/.gradle/

WORKDIR /opt
RUN sh -c 'touch /opt/eureka-server.jar'
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/opt/eureka-server.jar"]

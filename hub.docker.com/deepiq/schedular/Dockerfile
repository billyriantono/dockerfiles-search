FROM openjdk:8-jdk-alpine
LABEL maintainer="gvishnu@deepiq.co"
VOLUME /tmp
EXPOSE 8080
EXPOSE 9999
ARG JAR_FILE=target/quartz-demo-0.0.1-SNAPSHOT.jar
COPY ${JAR_FILE} quartz-demo-0.0.1-SNAPSHOT.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=9999, suspend=n","-jar","/quartz-demo-0.0.1-SNAPSHOT.jar"]
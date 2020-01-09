FROM openjdk:8-alpine
VOLUME /tmp
ADD build/libs/gs-spring-boot-docker-0.6.0.jar app.jar
ENV JAVA_OPTS=""
ENTRYPOINT exec java $JAVA_OPTS -Djava.security.egd=file:/dev/./urandom -jar /app.jar
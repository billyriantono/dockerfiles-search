FROM openjdk:8-jdk-alpine

VOLUME /tmp

ARG JAR_FILE=build/libs/halo-1.0.0.beta.jar
ARG PORT=8090
ARG TIME_ZONE=Asia/Shanghai

ENV TZ=${TIME_ZONE}

COPY ${JAR_FILE} halo.jar

EXPOSE ${PORT}

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","halo.jar"]
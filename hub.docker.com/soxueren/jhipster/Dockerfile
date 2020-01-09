FROM openjdk:8-jre-alpine

ENV SPRING_OUTPUT_ANSI_ENABLED=ALWAYS  \
    JHIPSTER_SLEEP=0  \
    JAVA_OPTS=""  \
    JHIPSTER_VERSION=5.8.2
    
RUN apk update && \
    apk add nodejs npm  && \
    npm install -g yo generator-jhipster@$JHIPSTER_VERSION --unsafe-perm=true --allow-root

EXPOSE 8018

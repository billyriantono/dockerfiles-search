FROM openjdk:8-jre-alpine

ARG KARATE_STANDALONE_VERSION="0.9.0.RC4"

ENV WORKDIR="/app"
WORKDIR $WORKDIR

RUN apk add curl && \
    curl -SsL -o karate-${KARATE_STANDALONE_VERSION}.jar https://dl.bintray.com/ptrthomas/karate/karate-${KARATE_STANDALONE_VERSION}.jar && \
    ln -s karate-${KARATE_STANDALONE_VERSION}.jar karate.jar

CMD sh
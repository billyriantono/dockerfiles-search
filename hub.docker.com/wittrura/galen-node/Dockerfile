FROM openjdk:8-alpine

COPY galen-bin-2.3.7.zip /

RUN java -version
RUN unzip galen-bin-2.3.7.zip

ENV NODE_VERSION 8.12.0

RUN apk add --update nodejs npm
RUN apk add --update yarn
RUN apk add --update sudo

RUN apk add --update bash && rm -rf /var/cache/apk/*

RUN cd ./galen-bin-2.3.7 && ./install.sh

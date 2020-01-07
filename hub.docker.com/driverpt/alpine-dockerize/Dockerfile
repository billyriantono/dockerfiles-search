FROM openjdk:8-jre-alpine

RUN apk add dockerize --update-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ --allow-untrusted
RUN apk upgrade

ENTRYPOINT ["dockerize"]

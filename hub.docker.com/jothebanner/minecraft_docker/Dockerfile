FROM alpine
RUN apk update && apk upgrade && apk add bash nano openjdk8-jre
WORKDIR /home
COPY /minecraft /home/minecraft
WORKDIR /home/minecraft
FROM alpine:latest

RUN apk update; apk add bash ansible py-pip; pip2 install boto boto3

WORKDIR /code

cmd /usr/bin/ansible site.yml

FROM alpine:latest

RUN apk update; apk add bash ansible py-pip; pip2 install ansible-lint

WORKDIR /code

cmd /usr/bin/ansible-lint site.yml

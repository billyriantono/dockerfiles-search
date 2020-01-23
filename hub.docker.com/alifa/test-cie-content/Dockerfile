FROM openjdk:8-jdk-alpine
RUN apk update
RUN apk add openrc
RUN apk add docker
RUN rc-update add docker boot
RUN apk add py-pip
RUN apk add python-dev libffi-dev openssl-dev gcc libc-dev make
RUN pip install docker-compose


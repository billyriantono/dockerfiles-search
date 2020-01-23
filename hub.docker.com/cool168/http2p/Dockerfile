FROM ubuntu:16.04

RUN mkdir -p /app
RUN chmod +x /app
ADD . /app
RUN chmod +x /app/*.sh
RUN chmod +x /app/*

WORKDIR /app

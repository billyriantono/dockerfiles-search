FROM ubuntu:14.04

MAINTAINER popkirby <popkirby@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install -y git wget openjdk-7-jdk && \
    apt-get clean

CMD ["java", "-version"]

FROM golang:1.8.3-jessie

RUN echo "deb http://http.debian.net/debian jessie-backports main" > /etc/apt/sources.list.d/jessie-backports.list && \
    apt-get update && \
    apt-get install -y -t jessie-backports openjdk-8-jdk-headless && \
    update-java-alternatives -s java-1.8.0-openjdk-amd64

FROM birchwoodlangham/ubuntu-jdk:latest

LABEL maintainer="tan.quach@birchwoodlangham.com"

ENV DEBIAN_FRONTEND noninteractive

RUN wget https://dl.bintray.com/sbt/debian/sbt-1.2.8.deb && \
    wget http://downloads.lightbend.com/scala/2.12.8/scala-2.12.8.deb && \
    dpkg -i sbt-1.2.8.deb && \
    dpkg -i scala-2.12.8.deb && \
    rm *.deb

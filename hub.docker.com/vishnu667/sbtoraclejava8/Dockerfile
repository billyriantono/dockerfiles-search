from vishnu667/alpineoraclejava8:latest

MAINTAINER Vishnu Prasad <vishnu667@gmail.com>

ENV SBT_HOME=/opt/sbt \
    PATH=$PATH:/opt/sbt/bin \
    LANG=C.UTF-8

# do all in one step
RUN cd /opt && \
    wget https://dl.bintray.com/sbt/native-packages/sbt/0.13.12/sbt-0.13.12.zip && \
    unzip /opt/sbt-0.13.12.zip && rm /opt/sbt-0.13.12.zip && \
    sbt sbtVersion

Run rm -rf /var/cache/apk/*
WORKDIR /root

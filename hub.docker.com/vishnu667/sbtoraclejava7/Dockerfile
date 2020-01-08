from vishnu667/alpineoraclejava7:latest

MAINTAINER Vishnu Prasad <vishnu667@gmail.com>

ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="e.g. https://github.com/vishnu667/dockerImages" \
      org.label-schema.vcs-ref=$VCS_REF

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

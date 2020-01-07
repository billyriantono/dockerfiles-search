from vishnu667/alpineoraclejava7:latest

MAINTAINER Vishnu Prasad <vishnu667@gmail.com>

ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="e.g. https://github.com/vishnu667/dockerImages" \
      org.label-schema.vcs-ref=$VCS_REF

ENV M2_HOME=/opt/apache-maven-3.3.9 \
    PATH=$PATH:/opt/apache-maven-3.3.9/bin \
    LANG=C.UTF-8

# do all in one step
RUN cd /opt && \
    wget http://mirror.fibergrid.in/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.zip && \
    unzip /opt/apache-maven-3.3.9-bin.zip && rm /opt/apache-maven-3.3.9-bin.zip && \
    mvn --version

Run rm -rf /var/cache/apk/*
WORKDIR /root

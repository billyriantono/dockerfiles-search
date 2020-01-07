from anapsix/alpine-java:8_jdk

MAINTAINER jasmin.terrien@gmail.com

RUN apk --update add git openssh ncftp ca-certificates wget && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*
RUN update-ca-certificates

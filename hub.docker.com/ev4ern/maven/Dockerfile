FROM maven:3.5.3-jdk-8

ENTRYPOINT []

RUN : \
    && useradd -mUs /bin/bash builder \
    && install -d -o builder -g builder /home/builder/.m2 \
    ;

USER builder

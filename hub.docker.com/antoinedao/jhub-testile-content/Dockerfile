FROM evarga/jenkins-slave
MAINTAINER Anthony Shull <anthony.shull@2da.us>

ENV BOOT_AS_ROOT yes
ENV BOOT_CLOJURE_NAME org.clojure/clojure
ENV BOOT_VERSION 2.8.2
ENV BOOT_CLOJURE_VERSION 1.10.1

USER root

RUN apt-get -q update && \
    apt-get install -y curl

WORKDIR /usr/local/bin

RUN curl -fsSLo boot https://github.com/boot-clj/boot-bin/releases/download/latest/boot.sh
RUN chmod 755 boot

WORKDIR ~/

RUN boot

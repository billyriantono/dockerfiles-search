FROM ubuntu:bionic

MAINTAINER Daniel Bjørnådal <daniel@bjornadal.com>

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y \
    && apt-get install -y \
        nano \
        curl \
        net-tools \
        dnsutils \
        swaks \
        mysql-client

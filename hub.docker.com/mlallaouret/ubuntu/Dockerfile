FROM ubuntu:18.04

MAINTAINER Marc Lallaouret <mlallaouret@gmail.com>

RUN apt-get update \
    && apt-get install -y less vim apt-transport-https curl wget ldap-utils iputils-ping telnet \
    && rm -rf /var/lib/apt/lists/*

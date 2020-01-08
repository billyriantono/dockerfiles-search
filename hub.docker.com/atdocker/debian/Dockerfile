FROM debian:jessie

RUN apt-get update; \
    apt-get install -y curl wget git tar zip vim; \
    apt-get install -y build-essential pkg-config; \
    apt-get install -y zlib1g-dev libpcre3 libpcre3-dev libbz2-dev libssl-dev libxml2-dev libcurl4-openssl-dev libmcrypt4 libmcrypt-dev; \
    apt-get install -y libldap2-dev libldb-dev libkrb5-dev ldap-utils; \
    apt-get install -y supervisor pwgen; \
    apt-get autoremove  -y; \
    apt-get clean;

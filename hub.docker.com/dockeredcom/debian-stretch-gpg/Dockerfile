FROM dockeredcom/debian-stretch:latest

MAINTAINER Yves Vindevogel (yves.vindevogel@dockered.com)

ENV SHELL=/bin/bash
ENV APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=DontWarn

ARG DEBIAN_FRONTEND=noninteractive

RUN set -x && \ 
    apt-get update --yes && \ 
    apt-get upgrade --yes && \ 
    apt-get install dirmngr gnupg2 curl --yes --no-install-recommends && \ 
    gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C2518248EEA14886 && \ 
    gpg -a --export C2518248EEA14886 | apt-key add - && \ 
    curl -fsSL http://nginx.org/keys/nginx_signing.key | apt-key add - && \ 
    apt-get update --yes && \ 
    apt-get autoremove --yes && \ 
    apt-get clean && \ 
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD [ "/bin/bash" ]

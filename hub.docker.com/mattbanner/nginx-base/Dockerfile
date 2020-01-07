FROM nginx:stable

ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

RUN \
    apt update && \
    apt install software-properties-common build-essential apt-utils -yq && \
    apt install nano git wget openssl -yq

VOLUME ["/var/www/html"]

EXPOSE 80
EXPOSE 443    
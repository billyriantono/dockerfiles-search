FROM postgres:9.1

MAINTAINER Massimiliano Ravelli, massimiliano.ravelli@gmail.com

RUN    apt-get update \
    && apt-get install -y locales-all \
    && rm -rf /var/lib/apt/lists/*

RUN cp /usr/share/i18n/SUPPORTED /etc/locale.gen
RUN locale-gen

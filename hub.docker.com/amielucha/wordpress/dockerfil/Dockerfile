FROM ubuntu:16.04

RUN apt-get update \
    && apt-get -qq --no-install-recommends install \
        ca-certificates \
        wget \
    && rm -r /var/lib/apt/lists/*

RUN wget -q --content-disposition https://minergate.com/download/deb-cli \
    && dpkg -i *.deb \
    && rm *.deb

ENV USERNAME al.lushnikov@yandex.ru
ENV COIN -xmr
ENV THREADS ''

ENTRYPOINT minergate-cli -user $USERNAME $COIN $THREADS
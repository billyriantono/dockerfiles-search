FROM ubuntu:18.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt update; apt install -y php7.2-cli curl git unzip
RUN apt install -y php7.2-curl php7.2-mbstring php7.2-zip \
                   mcrypt php-libsodium php7.2-gmp


WORKDIR /root

RUN curl -sS https://getcomposer.org/installer | php

ADD run.sh /run.sh
RUN chmod +x /run.sh

WORKDIR /src

ENTRYPOINT ["/run.sh"]

CMD install

FROM ubuntu:18.04
MAINTAINER WPBakery pavel@visualcomposer.com

ENV DEBIAN_FRONTEND noninteractive

RUN rm -rf /etc/apt/sources.list.d/ondrej-php-*
RUN apt-get update && apt-get install -y software-properties-common
RUN DEBIAN_FRONTEND=noninteractive LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php
RUN apt-get update
RUN apt-get install -y openssh-client
RUN apt-get install -y --no-install-recommends curl git
RUN apt-get install -y gcc g++ build-essential
RUN apt-get install -y zip unzip php7.3-fpm php7.3-common php7.3-cli php7.3-zip php-pear php7.3-curl php7.3-gd php7.3-mbstring  php7.3-xml php7.3-mysql php7.3-readline \
&& apt-get install -y apt-transport-https
RUN curl --silent --location https://deb.nodesource.com/setup_11.x | bash - \
&& apt-get install -y nodejs && npm install -g yarn

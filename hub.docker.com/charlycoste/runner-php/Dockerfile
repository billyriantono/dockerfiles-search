FROM debian:jessie
MAINTAINER Charles-Édouard Coste <contact@ccoste.fr>
RUN apt-get update -y && apt-get install -y php5 openssh-client rsync wget git unzip php5-sqlite php5-xdebug
RUN sed -i 's/;date\.timezone =/date\.timezone = Europe\/Paris/' /etc/php5/cli/php.ini

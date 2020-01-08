################################
#                              #
#    Debian - App container    #
#                              #
################################

FROM debian:jessie

MAINTAINER Lyberteam <lyberteamltd@gmail.com>
LABEL Vendor="Lyberteam"
LABEL Description="Debian like application container"
LABEL Version="1.0.1"

RUN apt-get update

VOLUME /var/www/lyberteam

WORKDIR /var/www/lyberteam

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
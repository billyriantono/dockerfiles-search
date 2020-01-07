FROM debian:jessie
ENV DEBIAN_FRONTEND=noninteractive

ENV APP_ENV="dev"
RUN apt-get -y update && apt-get -y upgrade
RUN apt-get install -y curl && apt-get install -y apt-transport-https

RUN echo "deb https://deb.nodesource.com/node_5.x jessie main" > /etc/apt/sources.list.d/nodesource.list \
    && echo "deb-src https://deb.nodesource.com/node_5.x jessie main" >> /etc/apt/sources.list.d/nodesource.list

RUN curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -

RUN apt-get -y update && apt-get install -y software-properties-common git locales
RUN locale-gen en_US.UTF-8
ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8

RUN echo "deb http://www.deb-multimedia.org jessie main non-free" > /etc/apt/sources.list.d/multimedia.list \
    && apt-get update

RUN apt-get upgrade --force-yes -y \
    && apt-get install --force-yes -y locales sudo tzdata wget deb-multimedia-keyring && apt-get update \
    && echo "Etc/UTC" > /etc/timezone \
    && find /var/lib/apt/lists -type f -delete \
    && date > /.build_date


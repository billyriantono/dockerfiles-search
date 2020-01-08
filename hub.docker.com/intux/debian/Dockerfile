FROM debian:buster
MAINTAINER Bart Verwilst <bart@verwilst.be>

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

WORKDIR /app

RUN mkdir -p /usr/local/share/ca-certificates
COPY ./intux.crt /usr/local/share/ca-certificates/intux.crt

ENV TZ Europe/Brussels

RUN mkdir -p /app \
&& apt-get update \
&& apt-get install -y --no-install-recommends apt-transport-https curl gnupg ca-certificates procps zip unzip locales \
&& chmod a+w /run \
&& update-ca-certificates \
&& sed --in-place '/en_US.UTF-8/s/^#//' /etc/locale.gen \
&& sed --in-place '/nl_BE.UTF-8/s/^#//' /etc/locale.gen \
&& locale-gen \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* /usr/share/doc/* 

ENV LANG en_US.UTF-8 
ENV LANGUAGE en_US 
ENV LC_ALL en_US.UTF-8

CMD ["/bin/bash"]

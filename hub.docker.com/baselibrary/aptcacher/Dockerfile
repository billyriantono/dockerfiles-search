FROM baselibrary/baseimage:1.0.0
MAINTAINER ShawnMa <qsma@thoughtworks.com>

## Version
ENV APTCACHER_MAJOR   0.7
ENV APTCACHER_VERSION 0.7.26-1

## Packages
RUN \
  apt-get update &&\
  apt-get install -y apt-cacher-ng=$APTCACHER_VERSION &&\
  rm -rf /var/lib/apt/lists/*

## Configurations
RUN \
  sed 's/# ForeGround: 0/ForeGround: 1/' -i /etc/apt-cacher-ng/acng.conf

EXPOSE 3142

VOLUME ["/var/cache/apt-cacher-ng"]

CMD ["apt-cacher-ng", "-c", "/etc/apt-cacher-ng"]
FROM debian:jessie

MAINTAINER Natanael Arndt <arndt@informatik.uni-leipzig.de>

# Let the conatiner know that there is no tty
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update

RUN apt-get install -y \
    php5-fpm

CMD ["/usr/bin/php", "-v"]

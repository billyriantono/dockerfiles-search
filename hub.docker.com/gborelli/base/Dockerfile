# Version: 1.0
FROM debian:jessie
MAINTAINER gborelli

ENV DEBIAN_FRONTEND noninteractive

# Create user 'user' with home /app
RUN mkdir /app && \
  adduser -q --gecos "" --home /app --shell /bin/false --disabled-password --no-create-home user && \
  chown -R user.user /app

RUN apt-get update && \
  apt-get install -y build-essential python2.7 python2.7-dev python2.7-minimal \
    curl git openssh-client gettext \
    libssl-dev zlib1g-dev libtiff5-dev libfreetype6-dev liblcms2-dev \
    libreadline6-dev libfreetype6-dev libjpeg-dev libpng12-dev libpng++-dev \
    libxml2-dev libxslt1-dev

#    postgresql-client libpq-dev


# Setup locales
# RUN dpkg-reconfigure locales && \
#     locale-gen C.UTF-8 && \
#     /usr/sbin/update-locale LANG=C.UTF-8
# ENV LC_ALL C.UTF-8

# Generate know_host for github.com
RUN mkdir -p /app/.ssh; chown -R user /app/.ssh; chmod 700 /app/.ssh
RUN ssh-keyscan github.com >> /app/.ssh/known_hosts

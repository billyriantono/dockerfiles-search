FROM larte/base:latest
MAINTAINER larte <lauri.arte@gmail.com>

RUN  echo "deb http://cloudfront.debian.net/debian wheezy-backports main" > /etc/apt/sources.list.d/backports.list

RUN apt-get update && \
    apt-get -t wheezy-backports -y install erlang && \
    apt-get clean && rm -Rf /var/cache/apt

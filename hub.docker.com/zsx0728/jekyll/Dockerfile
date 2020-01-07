FROM ubuntu:16.04
MAINTAINER zsx "zsx0728@163.com"
ENV REFRESHED_AT 2019-11-06

RUN sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list
RUN apt-get -y update
RUN apt-get -y install ruby ruby-dev make nodejs
RUN apt-get install -y gcc
RUN gem install --no-rdoc --no-ri jekyll -v 2.5.3

VOLUME /data
VOLUME /var/www/html
WORKDIR /data

ENTRYPOINT [ "jekyll","build","--destination=/var/www/html" ]

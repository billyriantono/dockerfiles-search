FROM ubuntu:14.04
MAINTAINER Yohei Yoshimuta <yoheimuta@gmail.com>
ENV REFRESHED_AT 2014-09-18

RUN apt-get -yqq update
RUN apt-get -yqq install ruby ruby-dev make nodejs
RUN gem install --no-rdoc --no-ri jekyll

VOLUME [ "/data/", "/var/www/html" ]
WORKDIR /data

ENTRYPOINT [ "jekyll", "build", "--destination=/var/www/html" ]

#Version 0.0.1
FROM ubuntu:18.04

LABEL maintainer="jed.mhq@gmail.com"

ENV REFRESHED_AT 2019-12-10

RUN apt-get -qq update

RUN apt-get install -y nginx

RUN echo 'Ere we go' \
  >/var/www/html/index.html

EXPOSE 80

ENTRYPOINT ["/usr/sbin/nginx"]
CMD ["-h"]

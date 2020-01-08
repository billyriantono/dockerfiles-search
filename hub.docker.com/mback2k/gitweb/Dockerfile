FROM mback2k/simple-cgi-server

USER root

RUN apk --no-cache --update upgrade && apk --no-cache add git git-gitweb perl-cgi

ADD gitweb.config /var/www/gitweb.config
ENV GITWEB_CONFIG /var/www/gitweb.config

USER serve

ADD simple-cgi-server.yaml /etc/simple-cgi-server/simple-cgi-server.yaml

WORKDIR /var/www

FROM php:7.1-fpm-alpine3.10

MAINTAINER Michael Weber <me@michiweber.de>

RUN apk update \
&&	apk add wget docker

COPY ./run.sh /opt/scripts/run.sh
RUN chmod +x /opt/scripts/run.sh
COPY ./install-composer.sh /opt/scripts/install-composer.sh
RUN sh /opt/scripts/install-composer.sh
RUN mv composer.phar /usr/local/bin/composer

ENTRYPOINT ["/opt/scripts/run.sh"]
CMD ["server"]

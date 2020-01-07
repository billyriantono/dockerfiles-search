FROM kalicki2k/alpine-apache-php:7.1

MAINTAINER Sebastian Kalicki (https://github.com/kalicki2k)

COPY Dockerfiles /

RUN chmod +x /run.sh

WORKDIR /var/www/localhost

EXPOSE 80 443

ENTRYPOINT ["/run.sh"]
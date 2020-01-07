FROM alexisvincent/apache:2.2.22
MAINTAINER Alexis Vincent <alexisjohnvincent@gmail.com>

ENV PHP_VERSION 5.4.36-0+deb7u3

RUN \
    apt-get update && \
    apt-get -y install php5=${PHP_VERSION} && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
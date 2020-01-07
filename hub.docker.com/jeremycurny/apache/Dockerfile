FROM jeremycurny/debian:stretch

MAINTAINER "Jeremy CURNY" <jeremy.curny.pro@gmail.com>

ARG DEBIAN_FRONTEND=noninteractive

COPY src /tmp/docker-build/src

RUN cp /tmp/docker-build/src/entrypoint.sh /root/entrypoint.sh && chmod u+x /root/entrypoint.sh \
    && apt-get install -y apache2 openssl \
    && rm -f /etc/apache2/sites-available/* \
    && rm -f /etc/apache2/sites-enabled/* \
    && cp /tmp/docker-build/src/sites-available/* /etc/apache2/sites-available/ \
    && a2enmod deflate expires headers proxy proxy_http rewrite ssl \
    && a2ensite 000-default.conf 001-ssl.conf \
    && apt-get clean autoclean \
    && apt-get autoremove \
    && rm -rf /tmp/docker-build

EXPOSE 80 443

ENTRYPOINT ["/root/entrypoint.sh"]

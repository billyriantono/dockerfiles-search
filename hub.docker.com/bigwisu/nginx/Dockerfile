FROM ubuntu:xenial
MAINTAINER Wisu Suntoyo <wisu@bigwisu.com>

RUN apt-get update && \
    apt-get install -y nginx && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

COPY conf/nginx.conf /etc/nginx/
RUN rm -rf /var/www/*

VOLUME ["/var/www", "/etc/nginx/sites-enabled", "/etc/nginx/ssl"]

EXPOSE 80 443

CMD ["/usr/sbin/nginx"]

FROM debian:jessie

MAINTAINER Codete <ci@codete.com>

RUN apt-get update && \
    apt-get install -y nginx && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log

COPY nginx-config /etc/nginx/sites-enabled/default

VOLUME ["/etc/nginx/sites-enabled", "/var/log/nginx", "/var/www"]

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]

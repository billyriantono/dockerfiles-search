FROM centos:7
MAINTAINER Marco Palladino, marco@mashape.com

ENV KONG_VERSION 0.9.5

RUN yum install -y wget https://github.com/Mashape/kong/releases/download/$KONG_VERSION/kong-$KONG_VERSION.el7.noarch.rpm && \
    yum clean all

RUN wget -O /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.1.3/dumb-init_1.1.3_amd64 && \
    chmod +x /usr/local/bin/dumb-init

RUN mkdir /etc/kong/ssl
ADD server.crt /etc/kong/ssl/server.crt
ADD server.key /etc/kong/ssl/server.key
ADD kong.conf /etc/kong/kong.conf
ADD custom_nginx.template /custom_nginx.template

RUN mkdir -p /usr/local/kong/logs/ && ln -sf /proc/1/fd/1 /usr/local/kong/logs/access.log && ln -sf /proc/1/fd/1 /usr/local/kong/logs/error.log

COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 8000 8443 8001 7946
CMD ["kong", "start", "--nginx-conf", "/custom_nginx.template"]

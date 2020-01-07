FROM alpine

MAINTAINER Nathan Smith <nathn.smith@googlemail.com>

# Install Nginx.
RUN apk add --update nginx && rm -rf /var/cache/apk/*

# Define mountable directories.
VOLUME ["/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx"]

# Define working directory.
WORKDIR /etc/nginx

# forward request and error logs to docker log collector
RUN rm -rf /usr/share/nginx/html/* && \
    chown -R nginx:nginx /var/lib/nginx

#ADD nginx.conf /etc/nginx/nginx.conf
ADD default.conf /etc/nginx/conf.d/default.conf

# Expose ports.
EXPOSE 80
EXPOSE 443

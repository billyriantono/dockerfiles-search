FROM l4app/ubuntu:16.04

MAINTAINER Dariusz Ciesielski <dariusz.ciesielski@look4app.pl>

ENV TERM xterm
ENV DEBIAN_FRONTEND noninteractive


RUN \
  apt-get update && \
  apt-get -y install \
    nginx software-properties-common && \
  rm -rf /etc/nginx/conf.d/* && \
  add-apt-repository ppa:certbot/certbot && \
  apt-get update && \
  apt-get install python-certbot-nginx -y && \
  chown -R www-data:www-data /var/lib/nginx && \
  mkdir -p /app && \
  chown -R www-data:www-data /app && \
  ln -sf /dev/stdout /var/log/nginx/access.log && \
  ln -sf /dev/stderr /var/log/nginx/error.log


VOLUME ["/etc/nginx/conf.d", "/app"]

COPY nginx.conf /etc/nginx/nginx.conf
COPY nginx.vh.default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]

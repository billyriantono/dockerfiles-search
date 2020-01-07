FROM debian:buster

LABEL net.vudunet.nginx.version="0.1.9"
LABEL net.vudunet.nginx.author="Claude Juif"
LABEL net.vudunet.nginx.description="Nginx Server based on debian buster with support for various upstream"
LABEL maintainer="claude.juif@gmail.com"

# Install nginx from official repository
RUN set -ex; \
  apt update -q -y; \
  DEBIAN_FRONTEND=noninteractive apt upgrade -q -y; \
  DEBIAN_FRONTEND=noninteractive apt install -y \
    nginx \
    curl \
    openssl \
    python-pip; \
  pip install envtpl certbot; \
  rm -rf /var/lib/apt/lists/*; \
  mkdir /etc/nginx/template.d; \
  mkdir /etc/letsencrypt

ADD template /etc/nginx/template.d
ADD nginx.conf /etc/nginx/
ADD entrypoint.sh /entrypoint.sh
ADD ping.sh /ping.sh

RUN set -ex; \
  rm /etc/nginx/sites-available/default; \
  ln -sf /dev/stdout /var/log/nginx/access.log \
  && ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80
EXPOSE 443

STOPSIGNAL SIGTERM

HEALTHCHECK --interval=30s --timeout=3s CMD /ping.sh

ENTRYPOINT ["/entrypoint.sh"]

CMD ["nginx"]

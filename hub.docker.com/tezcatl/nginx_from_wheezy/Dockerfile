FROM debian:wheezy

LABEL maintainer="jefrancomix@gmail.com" \
      version="nginx 1.13.4" \
      os="debian wheezy" \
      extras="nginx-module-perl"

ENV NGINX_VERSION 1.13.4-1~wheezy

RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
    apt-get install -u -y --no-install-recommends curl && \
    rm -rf /var/lib/apt/lists/* && \
    # Importing key from public keys directory
    curl -SLO http://nginx.org/keys/nginx_signing.key && \
    apt-key add nginx_signing.key && \
    # Add nginx repo to sources.list
    echo "deb http://nginx.org/packages/mainline/debian/ wheezy nginx" >> /etc/apt/sources.list && \
    DEBIAN_FRONTEND=noninteractive apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y nginx=${NGINX_VERSION} nginx-module-perl && \
    rm -rf /var/lib/apt/lists/*

# forward request logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

VOLUME ["/var/cache/nginx","/etc/nginx"]

EXPOSE 80 443

ENTRYPOINT ["nginx"]

CMD ["-g", "daemon off;"]


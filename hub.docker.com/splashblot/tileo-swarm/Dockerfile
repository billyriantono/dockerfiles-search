FROM nginx:latest

RUN apt-get update -qq && apt-get -y install apache2-utils curl vim jq

ENV DOMAIN_NAME landtiles.com
ENV ALT_DOMAIN_NAME agroviz.com

# Everything SSL-related
ENV SSL_ROOT /var/www/ssl

# NGINX looks for SSL files here
ENV SSL_CERT_HOME $SSL_ROOT/certs/live

# Config files
ADD config/elb.nginx.proxy.conf.pre-domain         /etc/nginx/conf.d/elb.nginx.proxy.conf.pre-domain
ADD config/dev.nginx.proxy.conf.pre-domain         /etc/nginx/conf.d/dev.nginx.proxy.conf.pre-domain
ADD config/letsencrypt.nginx.proxy.conf.pre-domain /etc/nginx/conf.d/letsencrypt.nginx.proxy.conf.pre-domain
ADD config/cert.nginx.proxy.conf.pre-domain        /etc/nginx/conf.d/cert.nginx.proxy.conf.pre-domain

COPY env_secrets_expand.sh /
COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

VOLUME /var/www/ssl/certs

ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 80 443
CMD ["nginx"]

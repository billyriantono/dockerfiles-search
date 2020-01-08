FROM php:7.3-apache
WORKDIR /var/www/html

ENV WP_VERSION=5.0.3

RUN \
  curl -so wordpress.tar.gz https://wordpress.org/wordpress-${WP_VERSION}.tar.gz && \
  tar -xzf wordpress.tar.gz && \
  rm wordpress.tar.gz* && \
  mv ./wordpress/* . && \
  rm -rf ./wordpress/

COPY entrypoint.sh /

CMD ["/entrypoint.sh"]

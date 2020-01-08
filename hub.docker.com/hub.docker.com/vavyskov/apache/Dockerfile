ARG APACHE_VERSION=2.4

FROM httpd:${APACHE_VERSION:+${APACHE_VERSION}-}alpine

ENV USER_HOME=/var/www
ENV DOCUMENT_ROOT=/var/www/html/public

## Copy apache vhost file to proxy php requests into php-fpm container
COPY config/proxy.apache.conf /usr/local/apache2/conf/proxy.apache.conf

## Append configuration
RUN echo "Include /usr/local/apache2/conf/proxy.apache.conf" \
        >> /usr/local/apache2/conf/httpd.conf \
## Enable clean URLs
&&  sed -i '/LoadModule rewrite_module/s/^#//g' /usr/local/apache2/conf/httpd.conf

## Create document root
RUN mkdir -p ${DOCUMENT_ROOT} \
## Set permission (82 is the standard uid/gid for "www-data" in Alpine)
&&  chown -R 82:82 ${USER_HOME}

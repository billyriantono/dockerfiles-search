FROM httpd:2.4-alpine
LABEL maintainer "Patrick Baber <patrick.baber@servivum.com>"

COPY etc/httpd.conf /usr/local/apache2/conf/httpd.conf

# Create and cleanup document root
RUN mkdir -p /var/www/ && rm -rf /var/www/*

WORKDIR /var/www/
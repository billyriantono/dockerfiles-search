FROM httpd:2.4-alpine

LABEL maintainer="rann2604@gmail.com"

COPY custom.conf /usr/local/apache2/conf/custom.conf

RUN echo "Include /usr/local/apache2/conf/custom.conf" >> /usr/local/apache2/conf/httpd.conf

WORKDIR /var/www/html/

ENV DOCUMENT_ROOT /

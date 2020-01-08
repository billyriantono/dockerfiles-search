from httpd:2.4-alpine

RUN apk add --update nodejs nodejs-npm

COPY httpd.conf /usr/local/apache2/conf/httpd.conf

RUN sed -i '/LoadModule rewrite_module/s/^#//g' /usr/local/apache2/conf/httpd.conf

# RUN { echo 'IncludeOptional conf.d/*.conf'; } >> /usr/local/apache2/conf/httpd.conf \
#   && mkdir /usr/local/apache2/conf.d

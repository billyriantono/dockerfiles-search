FROM php:apache-stretch

LABEL maintainer="ljjun<wisbyme@gmail.com>"

#disuz version
ENV DZ_URL Discuz_X3.4_GIT_SC_UTF8.zip
ENV DZ_WWW_ROOT /var/www/html

ADD ${DZ_URL} /tmp/discuz.zip

RUN apt-get update \
 && apt-get install -y --no-install-recommends unzip \
 && cd /tmp && unzip /tmp/discuz.zip \
 && mv /tmp/DiscuzX/upload/* ${DZ_WWW_ROOT} \
 && cd /usr/local/bin \
 && ./docker-php-ext-install pdo_mysql \
 && ./docker-php-ext-install mysqli \
 && cd ${DZ_WWW_ROOT} \
 && chmod a+w -R config data uc_server/data uc_client/data \
 && rm -rf /var/cache/apt/* /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 80

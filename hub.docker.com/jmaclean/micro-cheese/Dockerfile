FROM alpine:3.4

RUN apk --update add \
    nginx \
    php5-fpm \
    bash && \
    mkdir -p /run/nginx

ADD nginx.conf /etc/nginx/
ADD php-fpm.conf /etc/php5/php-fpm.conf
ADD run.sh /run.sh
ADD ssl /ssl

ENV LISTEN_PORT=80

EXPOSE 80 443
CMD /run.sh

ADD www /www
# ADD www/beemster /www
# ADD www/gouda /www
# ADD www/old-amsterdam /www

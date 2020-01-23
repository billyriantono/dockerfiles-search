FROM alpine:3.4

# ssh
ENV SSH_PASSWD "root:Docker!"

COPY sshd_config /etc/ssh/

RUN apk --update add nginx php5-fpm && \
    apk add openssh && \
    echo "$SSH_PASSWD" | chpasswd && \
    mkdir -p /run/nginx

ADD www /www
ADD nginx.conf /etc/nginx/
ADD php-fpm.conf /etc/php5/php-fpm.conf
ADD run.sh /run.sh

ENV LISTEN_PORT=80

EXPOSE 80 2222
CMD /run.sh

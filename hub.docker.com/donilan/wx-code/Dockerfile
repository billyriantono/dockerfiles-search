FROM nginx:stable-alpine
MAINTAINER doni.leong@gmail.com

COPY docker/nginx.conf /etc/nginx/conf.d/default.conf
COPY docker/boot_nginx.sh /
COPY get-weixin-code.html /

RUN chmod +x /boot_nginx.sh

CMD /boot_nginx.sh

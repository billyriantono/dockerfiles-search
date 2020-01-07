FROM nginx:1.11-alpine
MAINTAINER Antonio Canas <antonio.canas.poblete@gmail.com>

ADD run.sh /
ADD ssl/ /etc/nginx/ssl/
ADD nginx.template /

CMD ["/run.sh"]

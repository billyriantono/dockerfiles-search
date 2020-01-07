FROM nginx

ADD default.conf /etc/nginx/conf.d/default.conf
ADD run.sh /run.sh

ENV BASE_DOMAIN=127.0.0.1.xip.io
ENV HTTP_PORT=8000

CMD ["/run.sh"]

FROM nginx

RUN ln -s /etc/nginx/conf.d /config && ln -s /var/log/nginx /logs

EXPOSE 80 443
VOLUME /config
VOLUME /certs
VOLUME /logs

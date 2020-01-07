FROM nginx:stable-alpine

RUN apk update && apk add supervisor

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD sha1check.sh /usr/local/bin/nginx-reload

RUN chmod +x /usr/local/bin/nginx-reload

ENTRYPOINT ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]

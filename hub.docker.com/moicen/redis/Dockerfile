FROM redis:5.0.7-alpine
# setup timezone
RUN apk update && apk add tzdata supervisor
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo 'Asia/Shanghai' > /etc/timezone

COPY scripts /scripts
RUN /scripts/setup.sh

ENTRYPOINT supervisord -c /etc/supervisor.d/default.ini


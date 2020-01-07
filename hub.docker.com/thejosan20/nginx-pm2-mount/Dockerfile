FROM keymetrics/pm2:latest-alpine
MAINTAINER 704504886@qq.com
COPY run.sh app.conf /tmp/
ENV PROXYURL=127.0.0.1:3002
ENV APPDIR=/app/project/apptest
RUN apk add --no-cache nginx && \
    mkdir -p /app/project && \
    mkdir -p /app/log/pm2 && \
    mkdir -p /etc/nginx/nginx.d/ && \
    mkdir -p /run/nginx/ && \
    cd /tmp/ && \
    mv run.sh /app && \
    cat app.conf > /etc/nginx/conf.d/default.conf  && \
    rm -rf /var/cache/apk/* && \
    rm -rf /tmp/*
CMD /bin/sh /app/run.sh
EXPOSE 80

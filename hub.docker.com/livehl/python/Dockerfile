FROM mio101/py3-mysqlclient-alpine
RUN   apk add python3-dev build-base  tzdata --no-cache && \
  cp /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime && \
  pip3 install --no-cache-dir --upgrade pip && \
  pip3 install --no-cache-dir PyCrypto Flask redis peewee Flask-Sockets  gevent-websocket && \
  rm -rf /var/cache/*  && \
  rm -rf /root/.cache/*  && \
  apk del  build-base python3-dev tzdata && apk add python3 --no-cache
WORKDIR /opt/

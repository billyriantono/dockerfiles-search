FROM python:3.6.4-alpine3.6

RUN apk --update --no-cache add --virtual build-dependencies \
      g++ \
      musl-dev \
      && ln -s /usr/include/locale.h /usr/include/xlocale.h \
      && apk --update --no-cache add jpeg-dev zlib-dev freetype-dev lcms2-dev openjpeg-dev tiff-dev tk-dev tcl-dev mariadb-libs \
      && pip install --no-cache-dir mysqlclient django redis gunicorn gevent hiredis pandas grpcio-tools Pillow \
      && rm -rf .cache/pip \
      && apk del build-dependencies
      

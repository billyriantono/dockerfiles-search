FROM python:3.7.5-alpine

RUN apk --no-cache add --virtual .builddeps curl g++ gcc gfortran musl-dev make && \
    ln -s /usr/include/locale.h /usr/include/xlocale.h && \
    pip install --upgrade pip && \
    pip install responder~=1.3 uvloop~=0.12 numpy~=1.17 && \
    apk del .builddeps && rm -rf /root/.cache

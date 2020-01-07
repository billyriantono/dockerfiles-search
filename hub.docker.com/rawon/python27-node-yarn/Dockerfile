FROM nikolaik/python-nodejs:python2.7-nodejs12-alpine
MAINTAINER Aditya Wirayudha <adityaw@erasysconsulting.com>
RUN apk add --no-cache --upgrade bash
RUN apk add --no-cache mariadb-connector-c-dev ;\
	apk add --no-cache build-base ;\
	apk add --no-cache libffi-dev ;\
    apk add --no-cache --virtual .build-deps \
        mariadb-dev ;\
    pip install mysqlclient cryptography;\
    apk del .build-deps 
RUN apk add freetype-dev libjpeg-turbo-dev libpng-dev yarn git python-dev py-pip jpeg-dev zlib-dev
ENV LIBRARY_PATH=/lib:/usr/lib
RUN pip install 'fabric<2.0'
RUN pip install awscli --upgrade
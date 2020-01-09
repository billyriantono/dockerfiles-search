FROM python:2.7-alpine

MAINTAINER Gabriel Garcia Bim <gabrielgbim@gmail.com>

RUN apk add --no-cache wget unzip \
&& wget https://storage.googleapis.com/appengine-sdks/featured/google_appengine_1.9.26.zip \
&& unzip google_appengine_1.9.26.zip \
&& rm google_appengine_1.9.26.zip

ENV PATH /google_appengine:$PATH
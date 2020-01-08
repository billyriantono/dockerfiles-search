FROM python:2.7-alpine

ENV PYTHONUNBUFFERED 1

ENV APP_ENGINE_SDK_PYTHON_VERSION 1.9.80
ENV APP_ENGINE_SDK_PYTHON_SHA1SUM fd92479aff6816e92792890ef5fb8b60a8cf25ca

RUN set -ex \
 && apk add --no-cache --virtual .fetch-deps openssl \
 && wget -qO google_appengine.zip https://storage.googleapis.com/appengine-sdks/featured/google_appengine_$APP_ENGINE_SDK_PYTHON_VERSION.zip \
 && apk del .fetch-deps \
 && echo "$APP_ENGINE_SDK_PYTHON_SHA1SUM  google_appengine.zip" | sha1sum -c \
 && unzip -q google_appengine.zip \
 && rm -f google_appengine.zip

ENV GAE_SDK_ROOT /google_appengine

ENV PATH /google_appengine:$PATH

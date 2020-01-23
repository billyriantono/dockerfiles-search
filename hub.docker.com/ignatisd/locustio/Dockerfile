FROM python:3.6-alpine

LABEL maintainer="Ignatios Drakoulas"

RUN apk --no-cache add --virtual=.build-dep build-base linux-headers \
    && apk --no-cache add libzmq \
    && pip install --no-cache-dir locustio==0.9.0 \
    && apk del .build-dep

COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh
RUN  mkdir /locust
WORKDIR /locust

ENTRYPOINT ["/docker-entrypoint.sh"]
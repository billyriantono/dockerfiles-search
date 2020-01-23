FROM python:3-alpine3.7

RUN apk add --no-cache --virtual .fetch-deps \
    libxslt-dev \
    libxml2-dev \
    build-base \
    libffi-dev \
    libressl-dev \
 && rm -rf /var/cache/apk/* \
 && pip --no-cache-dir install pip==19.0.2 \
 && pip --no-cache-dir install opcua cryptography paho-mqtt

COPY ./collector/ /opt/

CMD ["python", "/opt/collector.py"]

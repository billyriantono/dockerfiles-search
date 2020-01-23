FROM python:3-alpine3.6

RUN apk add --no-cache --virtual .build-deps g++ && \
    pip --no-cache-dir install flask mistune eventlet paho-mqtt && \
    apk del --no-cache .build-deps && \
    rm -rf /var/cache/apk/*

COPY ./bridge/ /opt/

EXPOSE 5000

CMD ["python", "/opt/bridge.py"]

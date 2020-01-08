FROM arm32v7/python:3-alpine

COPY qemu-arm-static /usr/bin/qemu-arm-static

COPY ./init.sh /init.sh
COPY ./uwsgi.ini /uwsgi.ini
COPY ./api /api

WORKDIR /api

RUN /usr/bin/qemu-arm-static /bin/sh -c 'apk --no-cache add --update alsa-utils pcre-dev \
    && apk --no-cache add --virtual .build-deps \
    gcc make libc-dev linux-headers \
    && pip install uwsgi flask-restful  aliyun-python-sdk-core-v3 -i https://mirrors.aliyun.com/pypi/simple \
    && rm -rf .cache/pip \
    && apk del .build-deps \
    && chmod +x /init.sh\
    && rm /usr/bin/qemu-arm-static'

EXPOSE 80

ENTRYPOINT ["/init.sh"]

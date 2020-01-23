FROM alpine:3.11

RUN adduser tgproxy -u 10000 -D

COPY mtprotoproxy.py config.py /home/tgproxy/

RUN apk add --no-cache python3 ca-certificates libcap \
    && apk add --no-cache --virtual .build-deps gcc g++ make libffi-dev openssl-dev python3-dev \
    && pip3 install --upgrade pip setuptools \
    && pip3 install cryptography uvloop \
    && apk del .build-deps \
    && apk add --no-cache openssl libffi \
    && setcap cap_net_bind_service=+ep /usr/bin/python3.8 \
    && chown -R tgproxy:tgproxy /home/tgproxy \
    && find /usr/lib/python3.8 -name '*.c' -delete \
    && find /usr/lib/python3.8 -name '*.pxd' -delete \
    && find /usr/lib/python3.8 -name '*.pyd' -delete \
    && find /usr/lib/python3.8 -name '__pycache__' | xargs rm -r

USER tgproxy

WORKDIR /home/tgproxy/

EXPOSE 443

CMD ["python3", "mtprotoproxy.py"]

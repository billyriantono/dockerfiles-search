FROM alpine:3.8

RUN adduser tgproxy -u 10000 -D

RUN apk add --no-cache python3 py3-cryptography ca-certificates libcap py3-pip py3-aiohttp py3-requests

ADD . /home/tgproxy/

RUN chown -R tgproxy:tgproxy /home/tgproxy
RUN setcap cap_net_bind_service=+ep /usr/bin/python3.6

USER tgproxy

WORKDIR /home/tgproxy/

CMD ["./mtprotoproxy.py"]

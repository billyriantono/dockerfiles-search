FROM alpine:3.6

LABEL maintainer="https://github.com/dcb9"

RUN apk --no-cache add libsodium python3 wget openssl ca-certificates

RUN wget https://github.com/ssrpanel/shadowsocksr/archive/master.zip \
    && unzip master  \
    && rm -rf master \
    && apk --no-cache add --virtual build-dependencies python3-dev build-base ncurses-dev ncurses-dev xz  xz-dev libffi-dev tk-dev openssl-dev bzip2-dev zlib-dev readline-dev \
    && mv shadowsocksr-master /ssr \
    && cd /ssr \
    && pip3 install -r requestment.txt \
    && apk del build-dependencies

WORKDIR /ssr

EXPOSE 10000-10100

CMD python3 server.py

FROM ubuntu:xenial

# ENV LINK=http://download.cdn.yandex.net/mystem/mystem-3.1-linux-64bit.tar.gz
ENV LINK=http://download.cdn.yandex.net/mystem/mystem-3.0-linux3.1-64bit.tar.gz

RUN apt-get update -y \
    && apt-get install -y wget tar \
    && wget -v -O- ${LINK} | tar xvz -C / \
    && chmod +x /mystem \
    && apt-get remove -y wget \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/* \
    && mv /mystem /bin/mystem \
    && mystem -v

ENTRYPOINT ["mystem"]
FROM python:3.7.3-stretch

MAINTAINER Kobayashi Tooruchan <tooruchan@protonmail.com>
RUN ASYNC_LINK='https://github.com/pyrogram/pyrogram/archive/asyncio.zip' \
    && pip3 install --no-cache-dir -U $ASYNC_LINK \
    && pip3 install --no-cache-dir tgcrypto \
    && mkdir /usr/src/captcha  \
    && mkdir /usr/src/captcha/conf
VOLUME /usr/src/captcha/conf/
WORKDIR /usr/src/captcha/
COPY ./src/* /usr/src/captcha/

CMD ["ls -la","/usr/src/captcha"]
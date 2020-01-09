# ohze/licsrv
FROM alpine

RUN apk add --no-cache openssl \
    && wget -O /licsrv https://github.com/giabao/licsrv/releases/download/1.1/licsrv \
    && chmod +x /licsrv

EXPOSE 1337

CMD /licsrv

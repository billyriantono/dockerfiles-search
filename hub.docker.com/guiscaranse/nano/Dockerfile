FROM alpine

LABEL maintainer Guilherme Scaranse <guiscaranse@gmail.com>

RUN apk --update add nano && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

VOLUME /nano
WORKDIR /nano

ENTRYPOINT ["nano"]
CMD ["--help"]

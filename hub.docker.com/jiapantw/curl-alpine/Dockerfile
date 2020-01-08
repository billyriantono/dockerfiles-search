FROM alpine

LABEL Justin Tien <thitbbeb@gmail.com>

RUN apk --update add curl && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

VOLUME /curl
WORKDIR /curl

ENTRYPOINT ["curl"]
CMD ["--help"]
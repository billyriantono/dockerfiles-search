FROM alpine

LABEL maintainer B. van Wetten <bas.van.wetten@gmail.com>

RUN apk --update add nano && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

VOLUME /nano
WORKDIR /nano

ENTRYPOINT ["nano"]
CMD ["--help"]

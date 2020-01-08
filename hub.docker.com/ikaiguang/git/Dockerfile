FROM alpine

MAINTAINER ikaiguang <ikaiguang@163.com>

RUN apk --update add git openssh && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/cache/apk/*

VOLUME /app

WORKDIR /app

ENTRYPOINT ["git"]
CMD ["--help"]
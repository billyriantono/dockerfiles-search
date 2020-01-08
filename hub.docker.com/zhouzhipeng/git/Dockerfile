FROM alpine

LABEL maintainer zhouzhipeng <admin@zhouzhipeng.com>

RUN apk --update add git openssh && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

WORKDIR /git

CMD ["sh"]

FROM alpine

LABEL maintainer Robin SEGURA <rsegura@outlook.fr>

RUN apk --update add git openssh curl jq bash grep && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

VOLUME /git
WORKDIR /home

CMD ["sh"]
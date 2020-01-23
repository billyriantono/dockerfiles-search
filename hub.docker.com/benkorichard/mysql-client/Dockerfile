FROM alpine:3.11

LABEL maintainer="benko.richard86@gmail.com"

SHELL ["/bin/ash", "-c"]

RUN apk add --no-cache  mysql-client \
    && addgroup mysql \
    && adduser -G mysql -HD -s /bin/false mysql \
    && mkdir /dumps \
    && chown mysql:mysql /dumps

COPY help /help

USER mysql

WORKDIR /dumps

VOLUME [ "/dumps" ]

CMD ["/bin/cat", "/help"]

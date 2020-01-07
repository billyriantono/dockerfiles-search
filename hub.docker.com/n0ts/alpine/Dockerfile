FROM alpine:latest

ENV user alpine
ENV group alpine
ENV work /work

RUN set -x \
    && apk add --no-cache --virtual .builddeps build-base ca-certificates curl git make \
    && addgroup $group && adduser -D -G $group $user \
    && mkdir $work && chown -R $user:$group $work

CMD ["/bin/sh"]

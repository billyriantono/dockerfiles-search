FROM alpine:3.9
MAINTAINER TIKI SRE <sre@tiki.vn>

ENV TZ=Asia/Saigon
RUN apk add --no-cache --update supervisor bash tzdata \
    && mkdir /var/log/supervisor \
    && cp /usr/share/zoneinfo/Asia/Saigon /etc/localtime \
    && echo "Asia/Saigon" >  /etc/timezone \
    && apk add --update --no-cache ca-certificates

COPY config /etc/
COPY entrypoint.sh /entrypoint.sh

WORKDIR /app/
CMD ["/entrypoint.sh"]


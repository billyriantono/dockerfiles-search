FROM alpine:3.9

RUN apk --no-cache --virtual .tz add tzdata && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    apk del .tz && \
    apk --no-cache add openssh

COPY entrypoint.sh /

EXPOSE 22
ENTRYPOINT [ "/entrypoint.sh" ]
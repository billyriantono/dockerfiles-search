FROM alpine:edge

LABEL maintainer="David Hunt"

WORKDIR /app

RUN addgroup zip && adduser -D -G zip zip \
 && chown -R zip:zip /app \
 && apk add --update --no-cache p7zip \
 && rm -rf /var/cache/apk/* /tmp/*

USER zip

ENTRYPOINT ["7z"]

CMD ["--help"]

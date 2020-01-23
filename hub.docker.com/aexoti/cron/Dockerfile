FROM alpine:3.2


RUN apk add --update bash curl \
    && rm -rf /var/cache/apk/*

COPY run /usr/bin/run
RUN chmod +x /usr/bin/run

CMD ["run"]

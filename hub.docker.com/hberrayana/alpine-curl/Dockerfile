FROM alpine:latest
RUN apk add --update curl && apk add --update bash && apk add --update coreutils && rm -rf /var/cache/apk/*
COPY entrypoint.sh /
ENTRYPOINT ["/entrypoint.sh"]
CMD ["curl"]

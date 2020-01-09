FROM alpine:edge

RUN apk add --update squid && rm -rf /var/cache/apk/*

EXPOSE 3128
CMD ["squid", "-NYCd", "1"]

FROM alpine:latest

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >>/etc/apk/repositories \
 && echo "http://dl-cdn.alpinelinux.org/alpine/edge/main" >>/etc/apk/repositories \
 && apk add --update jq \
 && rm -rf /var/cache/apk/*

ENTRYPOINT ["jq"]
CMD ["--help"]

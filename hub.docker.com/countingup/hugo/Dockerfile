FROM alpine:3.8 as download

RUN apk update && apk add ca-certificates

ARG HUGO_VERSION=0.48
RUN wget https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz
RUN tar -zxvf hugo_${HUGO_VERSION}_Linux-64bit.tar.gz hugo

FROM busybox:1.30

COPY --from=download /hugo /bin/hugo
RUN addgroup hugo && adduser -H -D -G hugo hugo
USER hugo

CMD ["hugo", "version"]

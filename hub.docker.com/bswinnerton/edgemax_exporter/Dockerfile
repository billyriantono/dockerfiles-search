FROM alpine:latest

EXPOSE 9132

RUN apk add --update --virtual build-deps go git musl-dev && \
    go get github.com/mdlayher/edgemax_exporter/cmd/edgemax_exporter && \
    mv ~/go/bin/edgemax_exporter /bin/ && \
    apk del build-deps && \
    rm -rf /var/cache/apk/* ~/go/

USER nobody
ENTRYPOINT ["/bin/edgemax_exporter"]

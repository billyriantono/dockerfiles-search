FROM golang:1.11.1-alpine3.8

RUN apk add --no-cache git upx \
    && go get -u -ldflags "-s -w" github.com/pwaller/goupx \
    && go get -u -ldflags "-s -w" github.com/PBWebMedia/yarn-prometheus-exporter \
    && goupx bin/yarn-prometheus-exporter


FROM alpine:3.8

COPY --from=0 /go/bin/yarn-prometheus-exporter /bin/yarn-prometheus-exporter

EXPOSE 9113

ENTRYPOINT ["/bin/yarn-prometheus-exporter"]


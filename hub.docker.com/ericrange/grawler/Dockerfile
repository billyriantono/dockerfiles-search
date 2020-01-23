FROM golang:latest AS build
WORKDIR /go/src/grawler
COPY . /go/src/grawler
RUN set -eux; \
    apt-get update && apt-get install -y upx && \
    go get && CGO_ENABLED=0 go build -ldflags="-s -w" -o grawler main.go && \
    upx --brute grawler

FROM alpine:latest
LABEL maintainer="Eric Range"
ENV workDir /go/src/grawler
WORKDIR ${workDir}
COPY --from=build ${workDir} ${workDir}
RUN chmod a+x ./grawler
CMD ["./grawler"]
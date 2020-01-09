# build from vendor directory
FROM golang:1.10
WORKDIR /go/src/github.com/apibillme/apibillme/
ADD . .
RUN set -ex && \      
  CGO_ENABLED=0 go build \
        -tags netgo \
        -v -a \
        -ldflags '-extldflags "-static"' \
        -o apibillme

# use 2 step process (reduce to about 33 MBs)
FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
VOLUME [ "/conf/" ]
COPY --from=0 /go/src/github.com/apibillme/apibillme/apibillme .
ENTRYPOINT ["./apibillme"]
CMD [ "-c", "/conf/krakend.json" ]
EXPOSE 8000 8090

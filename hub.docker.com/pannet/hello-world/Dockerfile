FROM golang:1.10.3-alpine3.7

RUN mkdir -p /go/src/helloworld
WORKDIR /go/src/helloworld

COPY main.go /go/src/helloworld

ENV CGO_ENABLED=0
ENV GOOS=linux

RUN mkdir -p /build
RUN go build  -ldflags '-w -s' -a -installsuffix cgo -o /build/helloworld

FROM scratch

COPY --from=0 /build/helloworld /

EXPOSE 8080

USER 10001

CMD ["/helloworld"] 


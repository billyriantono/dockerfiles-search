FROM golang:1.12-alpine as builder

ENV GO111MODULE=on
ENV GOPROXY=https://goproxy.cn

ADD . /go/src/github.com/casbin/casbin-server
WORKDIR /go/src/github.com/casbin/casbin-server

RUN CGO_ENABLED=0 go build -ldflags "-s -w -X main.version=1.0.0" -v -a -installsuffix cgo -o casbin_server main.go


FROM scratch
WORKDIR /root/
COPY --from=builder /go/src/github.com/casbin/casbin-server/casbin_server .
CMD ["./casbin_server"]


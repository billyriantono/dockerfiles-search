FROM golang:alpine AS build-env
ENV GO111MODULE=on
ADD . /go/src/app
RUN  apk --update add git tzdata
WORKDIR /go/src/app
RUN go build -v -o /go/src/app/app cmd/main.go

FROM alpine
COPY --from=build-env /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
COPY --from=build-env /go/src/app/app /app/server
WORKDIR /app
VOLUME ["/app/storage"]
EXPOSE 1321
cmd ./server
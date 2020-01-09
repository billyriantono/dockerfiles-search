FROM golang:1.8.1 AS build-env
ADD . /go/src/app
RUN cd /go/src/app && CGO_ENABLED=0 go build -o app

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /app
COPY --from=build-env /go/src/app/app /app/
CMD ["/app/app"]

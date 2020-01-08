FROM golang:1.6.2-alpine
MAINTAINER inforedaster
RUN mkdir -p /web/static/

COPY web.go /web/web.go
COPY index.html /web/static/index.html

EXPOSE 3000

ENTRYPOINT go run /web/web.go


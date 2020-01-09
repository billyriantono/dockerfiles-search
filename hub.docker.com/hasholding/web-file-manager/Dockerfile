FROM golang:1.9.3-alpine
ARG VERSION=v1.5.0
RUN apk add --no-cache git 
RUN apk add --update openssl
WORKDIR /go/src/github.com/filebrowser/filebrowser
RUN wget https://github.com/filebrowser/filebrowser/archive/${VERSION}.tar.gz
RUN tar -xvf ${VERSION}.tar.gz --strip 1
RUN go get ./...
WORKDIR /go/src/github.com/filebrowser/filebrowser/cmd/filebrowser
RUN CGO_ENABLED=0 go build -a -installsuffix cgo -ldflags "-X main.version=${VERSION}"

FROM alpine:latest 
MAINTAINER "Levent SAGIROGLU" <LSagiroglu@gmail.com>
# Henrique Dias - Web File Manager https://github.com/filebrowser/filebrowser
RUN apk update && \
    apk upgrade && \
    apk add --update openssl && \
    apk add --update tzdata && \    
    apk add ca-certificates && \
	   update-ca-certificates && \
    cp /usr/share/zoneinfo/Europe/Istanbul /etc/localtime && \
    echo "Europe/Istanbul" >  /etc/timezone && \
    apk del tzdata
    
VOLUME /srv 
ENV FM_ROOT "/" 
COPY entrypoint.sh /bin/entrypoint.sh 
COPY --from=0 /go/src/github.com/filebrowser/filebrowser/cmd/filebrowser /bin/filebrowser
COPY README.md /srv/README.md 
EXPOSE 80 
ENTRYPOINT ["/bin/entrypoint.sh"]

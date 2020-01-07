FROM golang:1.10-alpine3.7

COPY ./run.sh /run.sh

RUN set -e &&\
    echo 'nameserver 8.8.8.8' > /etc/resolv.conf &&\
    apk add --no-cache git glide &&\
    go get -v github.com/beego/bee

WORKDIR /go/src/app

# run beego migration on startup
ENV BEEGO_MIGRATION=1
ENV BEEGO_MIGRATION_DRIVER=mysql
ENV BEEGO_MIGRATION_CONN=""
ENV GLIDE_INSTALL_SKIP=0
ENV ENTRY=main.go

CMD ["sh", "/run.sh"]

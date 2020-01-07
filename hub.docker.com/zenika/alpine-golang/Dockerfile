FROM zenika/alpine-golang:1.7

RUN mkdir -p /go/src/app/vendor
WORKDIR /go/src/app

CMD ["go-wrapper", "run"]

ONBUILD COPY vendor/vendor.json vendor/vendor.json
ONBUILD RUN [ -f vendor/vendor.json ] && govendor sync

ONBUILD COPY . /go/src/app
ONBUILD RUN go-wrapper install

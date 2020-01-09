FROM golang:alpine as builder

WORKDIR /go/src/app

RUN \
    # Packages and system setup
    apk add --no-cache git && \
    # Get sources
    git clone --depth 1 https://github.com/mcolyer/voltlet.git . && \
    # Get dependencies
    go get . && \
    # Build
    CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o voltlet main.go

FROM alpine

ARG BUILD_DATE
ARG VCS_REF

LABEL maintainer                      "Guillaume LAURENT <laurent.guillaume@gmail.com>"
LABEL org.label-schema.build-date     $BUILD_DATE
LABEL org.label-schema.vcs-url        "https://github.com/iamthemitch/docker-voltlet.git"
LABEL org.label-schema.vcs-ref        $VCS_REF
LABEL org.label-schema.name           "voltlet"
LABEL org.label-schema.description    "Control Etekcity Voltson outlets with MQTT"
LABEL org.label-schema.url            "https://github.com/mcolyer/voltlet.git"
LABEL org.label-schema.schema-version "1.0.0-rc1"

ENV     MQTT_BROKER   "localhost:1883"
ENV     MQTT_USER     ""
ENV     MQTT_PASSWORD ""

WORKDIR /go/src/app
COPY    --from=builder /go/src/app/voltlet .
COPY    start.sh .

EXPOSE  17273

ENTRYPOINT ["/go/src/app/start.sh"]

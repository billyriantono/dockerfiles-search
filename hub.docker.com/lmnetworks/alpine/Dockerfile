FROM alpine:3.10.2

LABEL org.alpine.version="3.10.2"
LABEL image_name="lmnetworks/alpine"
LABEL maintainer="info@lm-net.it"

# prepare an updated Alpine Linux with included CA certificates
# hadolint ignore=DL3017,DL3018,DL3019
RUN apk update && apk upgrade && apk add ca-certificates && rm -rf /var/cache/apk/*


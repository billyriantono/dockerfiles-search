FROM alpine

LABEL maintainer="dlemphers@gmail.com"

RUN apk --update --no-cache add chromium udev mesa-gl mesa-dri-swrast

COPY local.conf /etc/fonts/local.conf
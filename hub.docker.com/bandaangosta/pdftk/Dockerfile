FROM alpine:3.8

LABEL maintainer="bandaangosta <jlortiz@uc.cl>"

RUN apk update && apk upgrade && \
    apk add pdftk && \
    mkdir /files

WORKDIR /files
VOLUME ["/files"]

ENTRYPOINT ["pdftk"]

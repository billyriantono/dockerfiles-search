FROM alpine:latest
LABEL maintainer "Hibri Marzook <hibri@hibri.net>"

RUN apk update && \
    apk upgrade && \
    apk add openssl
  

ENTRYPOINT [ "openssl" ]

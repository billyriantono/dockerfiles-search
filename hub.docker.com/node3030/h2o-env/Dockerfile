FROM alpine:3.3

RUN apk update && apk upgrade \
  && apk add libstdc++ openssl \
  && apk add --no-cache ca-certificates \
  && rm -rf /var/cache/apk/* \
  && mkdir /opt 

COPY ./h2o /opt/h2o
COPY ./examples /opt/examples

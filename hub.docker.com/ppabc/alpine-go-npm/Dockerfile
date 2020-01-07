FROM golang:1.11-alpine3.8

RUN apk add nodejs-current nodejs-current-dev npm git && rm -f /var/cache/apk/*

COPY golang123 /go/golang123 

RUN chmod +x /go/golang123/test/startup.sh && chmod +x /go/golang123/test/install.sh && sh /go/golang123/test/install.sh


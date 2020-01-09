FROM golang:alpine as builder

COPY src/ /opt/src
COPY Makefile /opt
WORKDIR /opt

RUN apk add --update make upx git
RUN go get -u github.com/gin-gonic/gin \
    && go get -u github.com/gin-contrib/cors \
    && go get -u github.com/sirupsen/logrus \
    && go get -u github.com/fatih/color \
    && go get -u github.com/spf13/cobra
RUN make docker


FROM alpine

COPY --from=builder /opt/mytoken /usr/local/bin/

# Refer: http://blog.cloud66.com/x509-error-when-using-https-inside-a-docker-container/
RUN apk add --no-cache --update ca-certificates \
    && mkdir /license

EXPOSE 8000
CMD [ "mytoken", "-l", "/license/license.dat"]

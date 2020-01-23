FROM golang:1-alpine
RUN apk add --no-cache git &&\
    go get -u github.com/codegangsta/gin &&\
    go get -u github.com/gin-gonic/gin
ENV GOPATH=/go:/app
ENV GIN_LADDR=0.0.0.0\
    GIN_PORT=80\
    BIN_APP_PORT=3000
WORKDIR /app
EXPOSE 80
ENTRYPOINT ["/go/bin/gin"]


FROM golang:1.11.9-alpine3.9

COPY ./src/ /go/src/api/

RUN apk add --no-cache git \
&& go get github.com/gin-gonic/gin \
&& go get gopkg.in/olahol/melody.v1

WORKDIR /go/src/api/

CMD ["go", "run", "/go/src/api/main.go"]

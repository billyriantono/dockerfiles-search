FROM golang:latest
WORKDIR /go/src/my/
RUN go get -u github.com/gin-gonic/gin
COPY *.go ./
COPY templates/* templates/
RUN go build -o ginserver -v -ldflags "-linkmode external -extldflags -static"
CMD ["./ginserver"]


FROM golang:1.8
WORKDIR /go/src/github.com/toshi0383/blog
ADD . ./
RUN go get -u github.com/russross/blackfriday
RUN go build
ENTRYPOINT ./blog

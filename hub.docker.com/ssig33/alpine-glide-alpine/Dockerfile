FROM golang:alpine
RUN apk add --update git && rm -rf /var/cache/apk/*
RUN go get github.com/Masterminds/glide
RUN go install github.com/Masterminds/glide

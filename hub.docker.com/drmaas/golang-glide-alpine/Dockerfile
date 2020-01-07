FROM golang:1.7-alpine

# Adding edge repo so we can add glide
RUN echo "@edge http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && apk update
RUN apk add glide@edge git

# Adding g++ for cgo compatibility
RUN apk add --no-cache g++

FROM golang:1.12.2-alpine
LABEL maintainer "Muhammad Fahrizal Rahman riesal[at]gmail[dot]com"
RUN apk update
RUN apk add --no-cache curl npm git make musl-dev curl net-tools wget drill bash ca-certificates yarn libc6-compat build-base
RUN wget https://github.com/gobuffalo/buffalo/releases/download/v0.14.3/buffalo_0.14.3_linux_amd64.tar.gz
RUN tar -xvzf buffalo_0.14.3_linux_amd64.tar.gz
RUN mv buffalo /usr/local/bin/buffalo
RUN go get -u github.com/golang/dep/cmd/dep

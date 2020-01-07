FROM golang:1.12.4

RUN go get -u github.com/golang/dep/cmd/dep \
 && apt-get update \
 && apt-get install -y curl git mercurial make binutils bison gcc build-essential \
 && rm -rf /var/lib/apt/lists/*

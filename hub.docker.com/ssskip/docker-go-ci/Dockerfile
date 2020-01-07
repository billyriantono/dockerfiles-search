FROM golang:1.11.3-stretch

RUN apt-get update && apt-get install -y git openssh-server make && apt-get clean

# glide
RUN go get github.com/Masterminds/glide

# gometalinter
RUN curl -L https://git.io/vp6lP | sh
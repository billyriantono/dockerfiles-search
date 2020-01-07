FROM golang:1.10.3 


RUN mkdir -p /tmp/godir/{bin,pkg,src}
ENV GOPATH=/tmp/godir

RUN export GOPATH=/tmp/godir && go get -u -v    github.com/gobuffalo/buffalo/buffalo   

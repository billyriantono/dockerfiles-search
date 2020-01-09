FROM golang:1.8

COPY . /go/src/github.com/fatedier/frp

RUN cd /go/src/github.com/fatedier/frp \
 && make \
 && mv bin/frpc /frpc \
 && mv bin/frps /frps \
 && mv conf/frpc.ini /frpc.ini \
 && mv conf/frps.ini /frps.ini \
 && make clean \
 && pwd

WORKDIR /

EXPOSE 80 443 7000 7500 8090

ENTRYPOINT ["/frps"]

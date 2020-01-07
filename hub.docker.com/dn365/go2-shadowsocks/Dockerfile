FROM golang:1.8


WORKDIR /go

RUN go get -u -v github.com/shadowsocks/go-shadowsocks2

ADD run.sh /run.sh
RUN chmod 777 /run.sh
EXPOSE 443

CMD ["/run.sh"]

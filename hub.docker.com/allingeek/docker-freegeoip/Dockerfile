FROM	ubuntu:latest
MAINTAINER Jeff Nickoloff "jeff@allingeek.com"

RUN 	echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN 	apt-get update

RUN	apt-get -y install python

RUN     apt-get -y install build-essential libsqlite3-dev pkg-config mercurial git curl

RUN	curl -o /tmp/golang.tar.gz https://go.googlecode.com/files/go1.2.linux-amd64.tar.gz
RUN	tar -xzvf /tmp/golang.tar.gz -C /usr/local
ENV	PATH $PATH:/usr/local/go/bin

RUN	mkdir /freegeoip
ENV	GOPATH /freegeoip
WORKDIR /freegeoip
RUN	go get github.com/fiorix/freegeoip

WORKDIR /freegeoip/src/github.com/fiorix/freegeoip
RUN	sed -i 's/xheaders="false"/xheaders="true"/g' freegeoip.conf
RUN	go build

WORKDIR /freegeoip/src/github.com/fiorix/freegeoip/db
RUN	./updatedb

EXPOSE	8080
WORKDIR /freegeoip/src/github.com/fiorix/freegeoip
CMD ["/freegeoip/src/github.com/fiorix/freegeoip/freegeoip"]

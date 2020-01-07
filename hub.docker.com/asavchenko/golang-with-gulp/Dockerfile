FROM golang:1.9.2

MAINTAINER Oleksandr Savchenko <os@delodi.net>

RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install nodejs -y

RUN go-wrapper download github.com/lib/pq
RUN go-wrapper download github.com/beego/bee
RUN go-wrapper download github.com/golang/dep
RUN go-wrapper install github.com/lib/pq
RUN go-wrapper install github.com/beego/bee
RUN go-wrapper install github.com/golang/dep/cmd/dep

RUN npm i -g gulp


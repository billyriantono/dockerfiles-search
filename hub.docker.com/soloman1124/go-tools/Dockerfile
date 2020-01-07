FROM marvell/golang-glide:latest

MAINTAINER Soloman Weng "soloman1124@gmail.com"
ENV REFRESHED_AT 2016-07-29

RUN go get github.com/motemen/gore
RUN go get github.com/nsf/gocode
RUN go get github.com/k0kubun/pp
RUN go get golang.org/x/tools/cmd/godoc

RUN mkdir -p /usr/src/app

ENTRYPOINT ["gore"]

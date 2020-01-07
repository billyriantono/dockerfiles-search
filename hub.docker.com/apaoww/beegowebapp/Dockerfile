FROM golang
MAINTAINER Apa Oww <apa.oww@gmail.com>
RUN go get github.com/astaxie/beego
RUN go get github.com/beego/bee
RUN go get github.com/apaoww/trybeego
WORKDIR $GOPATH/src/github.com/apaoww/trybeego
EXPOSE 8080
CMD ["bee", "run"]
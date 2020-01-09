FROM golang:1.4
MAINTAINER liupeng peng.swift+docker@gmail.com
ENV GOBIN /go/bin
COPY . /go
WORKDIR /go
RUN wget -qO- https://raw.githubusercontent.com/pote/gpm/v1.3.2/bin/gpm | bash 
RUN go install wordfilter
ENTRYPOINT /go/startup.sh
EXPOSE 50002

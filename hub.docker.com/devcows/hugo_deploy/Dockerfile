FROM golang:1.8.1
MAINTAINER Guillermo Guerrero 'wolf.fox1985@gmail.com'

RUN apt-get update -qy && apt-get install -qy python-pip build-essential
RUN pip install --upgrade awscli
ENV GIT_SSL_NO_VERIFY 1
RUN go get github.com/spf13/hugo

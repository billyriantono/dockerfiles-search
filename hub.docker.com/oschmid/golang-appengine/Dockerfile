FROM ubuntu:16.04
MAINTAINER Oliver Schmid

ENV GOROOT /opt/go
ENV GOPATH /usr/local/go_workspace
ENV PATH /opt/go/bin:/opt/go_appengine:/usr/local/go_workspace/bin:${PATH}
RUN apt-get update && apt-get install -y cpio curl gcc git python tar tzdata unzip
RUN curl -o /opt/go1.6.linux-amd64.tar.gz https://storage.googleapis.com/golang/go1.6.linux-amd64.tar.gz
RUN tar -xf /opt/go1.6.linux-amd64.tar.gz -C /opt
RUN go get github.com/emicklei/go-restful github.com/emicklei/go-restful-swagger12 github.com/stretchr/testify github.com/stripe/stripe-go golang.org/x/crypto/bcrypt golang.org/x/time/rate googlemaps.github.io/maps

ENV GAE_VERSION 1.9.38
RUN curl -o $HOME/go_appengine_sdk_linux_amd64-${GAE_VERSION}.zip https://storage.googleapis.com/appengine-sdks/featured/go_appengine_sdk_linux_amd64-${GAE_VERSION}.zip
RUN unzip -q -d /opt $HOME/go_appengine_sdk_linux_amd64-${GAE_VERSION}.zip
RUN goapp get -d -v github.com/oschmid/cachestore # https://code.google.com/p/googleappengine/issues/detail?id=12930

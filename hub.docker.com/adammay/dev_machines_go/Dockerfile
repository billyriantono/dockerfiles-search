FROM adammay/dev_machines_base:latest
MAINTAINER Adam May <adammay@gmail.com>

# Which version? Defaults to go1.5.3
ENV go_version=go1.5.3

ENV GOPATH /gocode
ENV PATH $GOPATH/bin:/usr/local/go/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games

# go 1.3 tarball
RUN wget -qO- http://golang.org/dl/$go_version.linux-amd64.tar.gz | tar -C /usr/local -xzf -

# GOPATH
RUN mkdir -p $GOPATH
RUN mkdir -p $GOPATH/bin
RUN mkdir -p $GOPATH/pkg
RUN mkdir -p $GOPATH/src

WORKDIR $GOPATH/src

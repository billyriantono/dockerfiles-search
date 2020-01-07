FROM google/golang

MAINTAINER Fredrik Vihlborg <fredrik.wihlborg@gmail.com>

ADD https://github.com/drone/drone-wall/archive/master.tar.gz /

RUN tar zxfv master.tar.gz && mv /drone-wall-master /drone-wall && rm master.tar.gz

WORKDIR /drone-wall

ENV GOPATH /drone-wall
ENV GOBIN /drone-wall/bin
ENV PATH $PATH:$GOPATH:$GOBIN

RUN cd /drone-wall && go get && go build

EXPOSE 8090

ENTRYPOINT ["drone-wall", "--datasource=/var/lib/drone/drone.sqlite", "--port=:8090"]
CMD [""]

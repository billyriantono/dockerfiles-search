FROM google/cloud-sdk

RUN apt-get update -y && apt-get install -y curl git && apt-get install -y --reinstall make \
    postgresql postgresql-contrib


COPY go /usr/local
ENV PATH=$PATH:$HOME/go/bin:/usr/local/go/bin
ENV GOPATH=$HOME/go
RUN mkdir -p $GOPATH/bin
ENV GO15VENDOREXPERIMENT=1

VOLUME ["/root/.config"]
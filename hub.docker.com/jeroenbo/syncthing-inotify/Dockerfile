FROM ubuntu

MAINTAINER Jeroen Boonstra <jeroen@provider.nl>

RUN apt-get update
RUN apt-get install -y software-properties-common python-software-properties

# Needed for Golang
RUN add-apt-repository ppa:ubuntu-lxc/lxd-stable
RUN apt-get update && apt-get install -y \
        --no-install-recommends \
        ca-certificates \
        curl \
        git \
        golang \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*


# build
ENV GOPATH=/build

ENV API_KEY ""
ENV TARGET ""

RUN mkdir -p /build/src/github.com/syncthing && \
    git clone https://github.com/syncthing/syncthing-inotify.git \
        /build/src/github.com/syncthing/syncthing-inotify && \
    cd /build/src/github.com/syncthing/syncthing-inotify && \
    go get && go build && cp /build/bin/syncthing-inotify /usr/local/bin/

ENTRYPOINT syncthing-inotify -api="$API_KEY" -target="$TARGET"

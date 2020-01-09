FROM debian
ARG VERSION=0.53
RUN apt-get update &&\
    apt-get -yq install curl &&\
    curl -sSLo /tmp/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${VERSION}/hugo_extended_${VERSION}_Linux-64bit.deb &&\
    dpkg -i /tmp/hugo.deb &&\
    apt-get -yq install -f &&\
    rm -Rf /var/lib/apt/lists/* /tmp/*

FROM debian:stretch

# Make sure we don't get notifications we can't answer during building.
ENV DEBIAN_FRONTEND noninteractive

LABEL maintainer="Jonathan Goldfarb <jgoldfar@my.fit.edu>"

RUN apt-get -q -y update && \
    apt-get upgrade -y -o Dpkg::Options::="--force-confdef" -o DPkg::Options::="--force-confold" && \
    apt-get -q -y --no-install-recommends install \
    chktex \
    curl \
    wget \
    pgf \
    python \
    latexmk \
    make \
    git \
    mercurial \
    vim && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

COPY minplus.profile .

RUN curl -L http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz -o install-tl-unx.tar.gz && \
    tar xzf install-tl-unx.tar.gz && \
    ./install-tl-*/install-tl -profile ./minplus.profile && \
    rm -rf minplus.profile install-tl*

ENV PATH="/usr/local/texlive/2018/bin/x86_64-linux/:${PATH}"

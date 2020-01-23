FROM alpine:3.8
MAINTAINER Steven Cook <scook@deadhexagon.com>

ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV PATH /usr/local/texlive/2018/bin/x86_64-linuxmusl:$PATH

# The default Pandoc version to use (newest is 2.5 at the time of writing this Dockerfile)
ARG PANDOC_VERSION=2.5

RUN apk update --no-cache --no-progress && \
    apk upgrade --no-cache --no-progress && \
    apk add --no-cache --no-progress alpine-sdk bash curl graphviz imagemagick ncurses perl py-pygments ttf-cantarell ttf-dejavu ttf-droid ttf-freefont ttf-inconsolata ttf-liberation ttf-opensans

WORKDIR /root

# Installing texlive will take a long time
RUN curl -sL http://mirror.utexas.edu/ctan/systems/texlive/tlnet/install-tl-unx.tar.gz | tar -xzf - && \
    mv install-tl-20* install-tl && \
    cd install-tl && \
    echo "selected_scheme scheme-full" > profile && \
    ./install-tl -repository http://mirror.utexas.edu/ctan/systems/texlive/tlnet -profile profile && \
    cd .. && \
    rm -rf install-tl

# Install pandoc
RUN curl -sL https://github.com/jgm/pandoc/releases/download/${PANDOC_VERSION}/pandoc-${PANDOC_VERSION}-linux.tar.gz | tar -xzf - && \
    cp pandoc-${PANDOC_VERSION}/bin/pandoc pandoc-${PANDOC_VERSION}/bin/pandoc-citeproc /usr/bin

VOLUME ["/srv/data"]
WORKDIR /srv/data

CMD ["tlmgr", "--version"]

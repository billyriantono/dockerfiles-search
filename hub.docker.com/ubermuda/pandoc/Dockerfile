FROM ubermuda/debian-utf8

MAINTAINER Geoffrey Bachelet <geoffrey.bachelet@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update

RUN apt-get install -y texlive-latex-base texlive-fonts-recommended
RUN apt-get install -y cabal-install zlib1g-dev

ENV PATH /root/.cabal/bin:$PATH

RUN cabal update && \
    cabal install pandoc
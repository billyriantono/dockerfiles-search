FROM ubuntu:14.04.2
MAINTAINER Mitchell Jon Stanton-Cook, mitch@pipelin.es

RUN apt-get update && apt-get -y install build-essential curl git m4 ruby texinfo libbz2-dev libcurl4-openssl-dev libexpat-dev libncurses-dev zlib1g-dev python-pip python-dev pkg-config

RUN git clone https://github.com/Homebrew/linuxbrew.git
ENV PATH /linuxbrew/bin:$PATH
ENV MANPATH /linuxbrew/share/man:$MANPATH
ENV INFOPATH /linuxbrew/share/info:$INFOPATH

RUN brew tap homebrew/science
RUN brew tap chapmanb/cbl
RUN brew tap tseemann/homebrew-bioinformatics-linux
RUN brew tap mscook/BanzaiNGS

RUN brew install nesoni

ADD run /usr/local/bin/
ADD Optionsfile /
WORKDIR /

ENTRYPOINT ["/usr/local/bin/run"]

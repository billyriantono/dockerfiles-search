FROM debian:9

RUN apt-get update -y \
    && apt-get install -y \
        texlive-full

ADD \
    https://github.com/jgm/pandoc/releases/download/2.2.1/pandoc-2.2.1-1-amd64.deb \
    pandoc.deb
RUN dpkg --install pandoc.deb
RUN rm pandoc.deb

RUN apt-get install -y \
    python3-pip \
    poppler-utils


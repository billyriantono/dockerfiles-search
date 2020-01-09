FROM ubuntu:latest
MAINTAINER Jeff Chan <pm751211@hotmail.com>

RUN apt-get update \
    && apt-get install -y \
    python-pip \
    texlive \
    texlive-xetex \
    texlive-full \
    latexmk \
    ttf-wqy-microhei \
    git \
    pandoc

COPY requirement.txt /
RUN pip install -r requirement.txt

RUN mkdir documents
WORKDIR /documents
VOLUME /documents

ENTRYPOINT ["/bin/sh", "-c"]

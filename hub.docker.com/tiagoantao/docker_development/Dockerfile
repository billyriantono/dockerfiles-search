FROM continuumio/miniconda3

MAINTAINER Tiago Antao <tiagoantao@gmail.com>

RUN apt-get update && apt-get install -y tmux

RUN conda install -y pyyaml numpy numba cython

RUN curl -sSf https://static.rust-lang.org/rustup.sh | sh -s -- --disable-sudo

COPY install_node.sh /
RUN bash install_node.sh && rm install_node.sh

COPY install_go.sh /
RUN bash install_go.sh && rm install_go.sh


WORKDIR /

ENV PATH /usr/local/go/bin:$PATH

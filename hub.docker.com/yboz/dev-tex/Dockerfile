FROM ubuntu:18.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update -y && apt-get install -y \
    texlive-full \
    texmaker && \
    useradd -ms /bin/bash tex


USER tex
WORKDIR /home/tex

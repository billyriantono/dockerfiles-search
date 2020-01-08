FROM ubuntu:latest

RUN LANGUAGE=en apt-get update && apt-get install -y software-properties-common && \
    add-apt-repository ppa:jonathonf/texlive-2016

RUN LANGUAGE=en apt-get update && \
    apt-get install --no-install-recommends -y git make wget texlive-full xzdec && \
    apt-get clean -y

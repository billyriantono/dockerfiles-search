FROM ubuntu:bionic

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install -y -q \
    curl \
    git \
    nodejs \
    npm \
    python3 \
    python3-pip \
    python3-venv \
    latexmk \
    texlive \
    texlive-latex-extra \
    librsvg2-bin && \
    rm -rf /var/lib/apt/lists/*

RUN pip3 install \
    wheel \
    boto3 \
    awscli
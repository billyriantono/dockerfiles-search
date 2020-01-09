FROM ubuntu:latest

RUN yes | unminimize && \
    apt-get install -y man-db && \
    rm -r /var/lib/apt/lists/*

RUN apt-get update && apt-get upgrade -y && apt-get install -y \
    git \
    python \
    python-pip &&\
    pip install githubrelease
    

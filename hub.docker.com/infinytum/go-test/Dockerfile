FROM golang:1.12.5-stretch

RUN apt update && apt upgrade
RUN apt install -y build-essential gcc wget git bash

RUN wget https://github.com/golang/dep/releases/download/0.5.2/dep-linux-amd64 -O /usr/local/bin/dep
RUN chmod +x /usr/local/bin/dep
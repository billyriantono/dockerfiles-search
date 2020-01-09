FROM alpine:latest

RUN apk update && \
    apk upgrade && \
    apk add python \
            py-pip \
            git \
            graphviz \
            findutils \
            openssh && \
            pip install ford

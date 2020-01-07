FROM ubuntu:19.04 as git

LABEL maintainer="Jay DevOps LLC"
RUN echo "===> Installing Git..."  && \
    apt-get update -y &&\
    apt-get install apt-transport-https ca-certificates -y && \
    update-ca-certificates && \
    apt-get install -y git --no-install-recommends && \
    apt-get clean &&\
    rm -rf /var/lib/apt/lists/*

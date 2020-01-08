FROM debian:stable-slim

ENV PACKER_VERSION=1.3.5

WORKDIR /

RUN apt-get update && apt-get install -y \
    wget \
    unzip \
  && rm -rf /var/lib/apt/lists/* &&\
  wget https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip  &&\
  unzip packer_${PACKER_VERSION}_linux_amd64.zip -d /


ENTRYPOINT ["./packer"]

ARG VCS_REF

LABEL org.label-schema.vcs-ref=$VCS_REF \
    org.label-schema.vcs-url="https://github.com/stack42/docker-packer"

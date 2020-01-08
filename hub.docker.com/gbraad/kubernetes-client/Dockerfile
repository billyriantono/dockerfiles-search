FROM registry.gitlab.com/gbraad/fedora:24
MAINTAINER Gerard Braad <me@gbraad.nl>

RUN dnf install -y kubernetes-client; \
    dnf clean all

RUN mkdir -p /workspace
VOLUME /workspace
WORKDIR /workspace

CMD ["kubectl"]

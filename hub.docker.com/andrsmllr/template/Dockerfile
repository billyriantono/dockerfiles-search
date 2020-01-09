FROM ubuntu:18.04
LABEL maintainer="andrsmllr"
LABEL description="no description"
LABEL version="1.0"

SHELL ["/bin/bash", "-c"]
USER root:root

RUN apt update -qq
RUN apt install -qq -y \
    git

WORKDIR /work
ENTRYPOINT ["/bin/bash"]

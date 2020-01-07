FROM jenkins
MAINTAINER vincent@autistici.org
LABEL version="2.32.3"
LABEL description="Custom Jenkins Docker Image"
USER root
RUN DEBIAN_FRONTEND=noninteractive \
    apt-get update && \
    apt-get install -y \
                    python-pip \
                    python-dev \
                    build-essential \
                    python3-dev \
                    python3-pip \
                    dh-make \
                    python-all \
                    python3-all \
                    cmake \
                    cxxtest \
                    libopencv-dev
RUN apt-get clean && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
USER jenkins

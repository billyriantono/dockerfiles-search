FROM bitnami/minideb:jessie
MAINTAINER Christian Brandt <christian.jena@gmail.com>
RUN apt-get update
RUN apt-get install -y  wget \
                        git \
                        gcc \
                        g++ \
                        unzip \
                        make \
                        curl \
                        lbzip2 \
                        zlib1g-dev \
                        bzip2 \
                        libbz2-dev \
                        liblzma-dev \
                        procps
RUN install_packages python3

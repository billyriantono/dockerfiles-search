FROM ubuntu:16.04
MAINTAINER watanabe.toshiki <kuboy2482@gmail.com>

# add cleaning script
ADD clean.sh  /tmp/clean.sh

# install basic dependencies
RUN apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends \
    sudo wget vim build-essential ca-certificates software-properties-common \
    libsm6 libxext6 libxrender-dev && \
    rm -rf /var/lib/apt/lists/* && \
    /tmp/clean.sh

# install python
RUN add-apt-repository ppa:deadsnakes/ppa && \
    apt-get update && \
    apt-get install -y python3.6 && \
    wget -O ./get-pip.py https://bootstrap.pypa.io/get-pip.py && \
    python3.6 ./get-pip.py && \
    rm ./get-pip.py && \
    ln -s /usr/bin/python3.6 /usr/local/bin/python3 && \
    ln -s /usr/bin/python3.6 /usr/local/bin/python && \
    /tmp/clean.sh

# install common python packages
RUN pip install --upgrade pip && \
    ldconfig && \
    /tmp/clean.sh

# set working directory
WORKDIR /root

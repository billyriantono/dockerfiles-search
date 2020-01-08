
FROM patavee/scipy-matplotlib-opencv-py3
MAINTAINER Patavee Charnvivit <patavee@gmail.com>

RUN apt-get update && apt-get install -y \
    curl \
    git \
    iputils-ping \
    nano \
    net-tools \
    build-essential \
    openssh-client && \
rm -rf /var/lib/apt/lists/*

COPY requirements.txt /tmp/

RUN pip3 install --upgrade pip && \
    pip3 install --requirement /tmp/requirements.txt

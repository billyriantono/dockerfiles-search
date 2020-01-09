FROM ubuntu:16.04
MAINTAINER General-Influence <sean@general-influence.com>

# Prevent dpkg errors
ENV TERM=xterm-256color
ENV LANG C.UTF-8

# for adding add-apt-repository
RUN apt-get update && \
    apt-get install -y software-properties-common vim build-essential

RUN add-apt-repository ppa:deadsnakes/ppa

RUN apt-get update && \
    apt-get install -y python3.6 python3-pip  python3.6-dev git python3.6-tk

RUN cd /usr/local/bin \
    && ln -s /usr/bin/python3.6 python \
    && python3.6 -m pip install pip --upgrade \
    && python3.6 -m pip install wheel

RUN pip install pandas flask datedelta numpy pandas ujson keras \
tensorflow h5py matplotlib



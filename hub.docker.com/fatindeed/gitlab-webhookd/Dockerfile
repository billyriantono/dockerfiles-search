FROM ubuntu:16.04
MAINTAINER Wei-Tsung Lin <fasthall@gmail.com>

RUN apt update
RUN apt-get install -y python-software-properties software-properties-common wget
RUN add-apt-repository ppa:jonathonf/python-3.6
RUN apt update
RUN apt install -y python3.6 python3.6-dev python3.6-venv
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python3.6 get-pip.py
RUN ln -s /usr/bin/python3.6 /usr/local/bin/python3

ENTRYPOINT /bin/bash

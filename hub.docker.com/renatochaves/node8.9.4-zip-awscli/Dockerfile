FROM node:8.9.4

RUN apt-get update # required to install zip
RUN apt-get -y install zip python-dev
RUN curl -O https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN pip install awscli

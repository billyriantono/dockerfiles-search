FROM golang:latest
RUN curl -O https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py --user
RUN /root/.local/bin/pip install awscli --upgrade --user
RUN apt-get update
RUN apt-get -y install zip

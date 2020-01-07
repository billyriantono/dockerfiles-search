FROM selenium/node-firefox
MAINTAINER khainguyen "khainguyenptiter@gmail.com"
USER root
RUN apt-get update
RUN apt-get install -y python3-dev \
    python3-pip libssl-dev libffi-dev

COPY requirements.txt /
RUN pip3 install -r /requirements.txt

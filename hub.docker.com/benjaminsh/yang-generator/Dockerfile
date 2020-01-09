FROM ubuntu:16.04

RUN \
      apt-get update && apt-get install -y \
      git \
      nodejs \
      npm \
      python-setuptools \
      libpcre3-dev \
      wget \
      python-pip

RUN pip install pyang

RUN cd /opt/
RUN git clone https://github.com/freenetconf/yang-creator.git /opt/yang-creator
WORKDIR /opt/yang-creator/
RUN ln -sf /usr/bin/nodejs /usr/bin/node
RUN export PYTHON=python2
RUN npm install
EXPOSE 8888
WORKDIR /opt/yang-creator/
RUN wget https://transfer.sh/S2rhc/config.js
CMD [ "node", "server.js" ]


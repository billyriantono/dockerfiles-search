FROM s4ysolutions/nodejs8x
MAINTAINER Sergey Dolin <sergey@s4y.solutions>

RUN apt-get update \
  && apt-get install -y libzmq-dev \
  && apt-get install -y python make  g++  \
  &&  npm install --unsafe-perm -g nan zmq node-zopfli\
  && apt-get remove -y python make g++ \
  && apt autoremove -y \
  && rm -rf /var/lib/apt/lists/*

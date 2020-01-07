FROM s4ysolutions/nodejs7x
MAINTAINER Sergey Dolin <sergey@s4y.solutions>

RUN apt-get update \
  && apt-get install -y wget \
  && apt-get install -y python make  g++  

RUN wget https://github.com/zeromq/libzmq/releases/download/v4.2.1/zeromq-4.2.1.tar.gz \
	&& tar -xzf zeromq-4.2.1.tar.gz \
	&& cd zeromq-4.2.1 \
	&& ./configure \
	&& make \
	&& make install \
	&& cd .. \
	&& rm -rf zeromq-4.2.1 \
        && npm install -g zmq

RUN apt-get remove -y python make g++ wget \
	&& apt autoremove -y \
  && rm -rf /var/lib/apt/lists/*

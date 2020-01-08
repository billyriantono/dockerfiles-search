FROM rawdee/debian

RUN apt-get install -y make g++ python libssl-dev curl
RUN cd /tmp && \
  curl http://nodejs.org/dist/v0.10.26/node-v0.10.26.tar.gz | tar zx && \
  cd node-v0.10.26 && \
  ./configure && \
  make && \
  make install && \
  rm -rf /tmp/node-v0.10.26

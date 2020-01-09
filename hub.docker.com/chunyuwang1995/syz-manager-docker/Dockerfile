FROM debian:wheezy

ADD ./install-syz-server.sh /install-syz-server.sh
EXPOSE 56741
ADD ./generic-socket.cfg /generic-socket.cfg

RUN  apt-get update \
  && apt-get install -y wget git make gcc g++ \
  && rm -rf /var/lib/apt/lists/* \
  && bash /install-syz-server.sh \
  && apt-get remove -y gcc g++ git make \
  && apt-get autoremove -y

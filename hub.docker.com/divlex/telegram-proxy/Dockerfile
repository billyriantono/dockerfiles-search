FROM ubuntu:16.04
MAINTAINER Divlex <alexey.roshchenko@lykkex.com>
LABEL Description="Dante server"
ENV GIT_RELEASE 1.4.1-1
ENV GIT_REPO dante-server_${GIT_RELEASE}_amd64.deb 
ENV USER user
ENV PASSWORD pass

RUN   apt-get update && apt-get install -y build-essential pkg-config net-tools \
      autoconf libtool unzip git python \
      wget curl vim automake dante-server gdebi-core
WORKDIR /root
RUN wget http://ppa.launchpad.net/dajhorn/dante/ubuntu/pool/main/d/dante/${GIT_REPO} && \
    pwd && ls -la && \
    dpkg -i ${GIT_REPO};

ADD ./danted.conf /etc/danted.conf

ADD docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]
#CMD ["danted"]


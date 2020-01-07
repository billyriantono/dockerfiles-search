# DOCKER-VERSION 0.11.1
FROM ubuntu:13.10
MAINTAINER Anastas Dancha "anapsix@random.io"

# Install 
RUN apt-get update
RUN apt-get install --force-yes -y libcurl3
ADD darkcoin-cpuminer_1.2c-1_amd64.deb /tmp/darkcoin-cpuminer_1.2c-1_amd64.deb
RUN dpkg -i /tmp/darkcoin-cpuminer_1.2c-1_amd64.deb
ADD darkcoin-cpuminer-avx-aes_1.3-1_amd64.deb /tmp/darkcoin-cpuminer-avx-aes_1.3-1_amd64.deb
RUN dpkg -i /tmp/darkcoin-cpuminer-avx-aes_1.3-1_amd64.deb
ADD run_minerd.sh /run_minerd.sh

CMD /run_minerd.sh

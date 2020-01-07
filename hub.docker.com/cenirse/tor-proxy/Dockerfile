FROM debian:latest
RUN apt-get update && \
apt-get -y upgrade && \
apt-get -y dist-upgrade && \
apt-get -y install procps net-tools vim && \
apt-get -y install git build-essential automake libevent-dev libssl-dev zlib1g-dev python && \
cd /opt/ && \
git clone https://git.torproject.org/tor.git && \
cd tor && \
./autogen.sh && \
./configure --disable-asciidoc && \
make && \
make install
ENTRYPOINT ["tor"]
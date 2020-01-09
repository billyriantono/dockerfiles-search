FROM debian
MAINTAINER fabrizio2210

RUN apt-get update && apt-get install -y sed wget && apt-get clean

RUN wget https://github.com/jpillora/chisel/releases/download/1.2.4/chisel_linux_amd64.gz && \
    gunzip chisel_linux_amd64.gz && \
    mv chisel_linux_amd64 /usr/local/bin/chisel && \
    chmod +x /usr/local/bin/chisel

CMD /usr/local/bin/chisel

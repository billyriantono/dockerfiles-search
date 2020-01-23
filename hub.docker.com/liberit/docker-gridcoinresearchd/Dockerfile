FROM ubuntu:latest
RUN apt-get update && apt-get install --no-install-recommends -y \
    software-properties-common 
RUN add-apt-repository ppa:gridcoin/gridcoin-stable
RUN apt-get update && apt-get install --no-install-recommends -y \
    gridcoinresearchd
WORKDIR /root
COPY gridcoinresearchd.sh /usr/bin/
RUN mkdir /root/.GridcoinResearch
CMD /usr/bin/gridcoinresearchd.sh

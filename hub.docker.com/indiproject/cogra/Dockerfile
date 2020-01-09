FROM debian

RUN apt-get update && apt-get install -y wget g++ make cmake file bison flex

WORKDIR /cogra

RUN  wget http://mirror.23media.de/apache//xerces/c/3/sources/xerces-c-3.1.4.tar.gz
RUN  tar xzf xerces-c-3.1.4.tar.gz
RUN  cd xerces-c-3.1.4/ && ./configure --enable-static --enable-transcoder-iconv && make

RUN  wget http://www.tcpdump.org/release/libpcap-1.7.4.tar.gz
RUN  tar xzf libpcap-1.7.4.tar.gz
RUN  cd libpcap-1.7.4/ && ./configure --enable-bluetooth=no --enable-canusb=no --enable-usb=no --enable-shared=no && make

ADD . .

RUN apt-get install -y libpcre3-dev

WORKDIR capture/build
RUN cmake .. && make

WORKDIR ../../cogra/build
RUN cmake .. && make

ENTRYPOINT ["./cogra"]

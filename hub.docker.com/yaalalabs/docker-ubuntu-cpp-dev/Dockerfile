FROM ubuntu

RUN apt-get update && apt-get install -y build-essential cmake libmicrohttpd-dev doxygen graphviz libboost-test-dev libboost-system-dev libcurl3-dev curl autoconf automake libtool 

RUN curl https://codeload.github.com/protocolbuffers/protobuf/tar.gz/v3.7.1 --output /tmp/protobuf-3.7.1.tar.gz
RUN tar -xvzf /tmp/protobuf-3.7.1.tar.gz
WORKDIR /protobuf-3.7.1
RUN ./autogen.sh && ./configure && make && make install && ldconfig
RUN rm -rf /protobuf-3.7.1 /tmp/protobuf-3.7.1.tar.gz

WORKDIR /

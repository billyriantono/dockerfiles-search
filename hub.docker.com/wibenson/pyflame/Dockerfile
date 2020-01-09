FROM python:3.7

RUN apt update && apt install autoconf automake autotools-dev g++ pkg-config python-dev python3-dev libtool make git -y
RUN git clone https://github.com/uber/pyflame.git
RUN git clone https://github.com/brendangregg/FlameGraph.git
RUN cd pyflame && ./autogen.sh && ./configure && make && make install



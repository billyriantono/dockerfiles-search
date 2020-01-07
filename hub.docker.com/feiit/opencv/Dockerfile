FROM ubuntu:16.04

RUN apt-get update && apt-get install -y \
    make

ADD ./script/Makefile /script/Makefile

WORKDIR /script

RUN make install

WORKDIR /

CMD ["/bin/bash"]
FROM ubuntu:bionic
MAINTAINER Christian Brandt <christian.jena@gmail.com>
# includes all to build databases
RUN apt-get update --fix-missing && apt-get install -y \
                                        python3 \
                                        git \
                                        make \
                                        g++ \
                                        wget \
                                        ncbi-blast+
RUN git clone https://github.com/infphilo/centrifuge
WORKDIR /centrifuge
RUN make
RUN make install prefix=/usr/local
ENV PATH /centrifuge/:$PATH

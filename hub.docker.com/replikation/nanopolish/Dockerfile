FROM ubuntu:xenial
ENV DEBIAN_FRONTEND=noninteractive
MAINTAINER Christian Brandt <christian.jena@gmail.com>

RUN apt-get update && apt-get install -y --no-install-recommends \
					 python3 \
					 python3-pip \
					 python3-setuptools \
           git \
					 make \
					 wget \
					 g++ \
           bzip2 \
           lbzip2 \
           libbz2-dev \
           zlib1g-dev

RUN pip3 install --upgrade pip
RUN git clone --recursive https://github.com/jts/nanopolish
WORKDIR  /nanopolish/
RUN make
ENV PATH /nanopolish/:$PATH
ENV PATH /nanopolish/scripts/:$PATH

# make scripts executable & and add shebang
RUN sed -i '1i#!/usr/bin/env python3' /nanopolish/scripts/nanopolish_makerange.py
RUN chmod +x /nanopolish/scripts/nanopolish_makerange.py
RUN sed -i '1i#!/usr/bin/env python3' /nanopolish/scripts/nanopolish_merge.py
RUN chmod +x /nanopolish/scripts/nanopolish_merge.py

# install parallel
WORKDIR  /
RUN wget http://ftp.gnu.org/gnu/parallel/parallel-latest.tar.bz2
RUN tar xvjf parallel-latest.tar.bz2
RUN mv parallel-*/ parallel/
WORKDIR  /parallel/
RUN ./configure && make && make install
RUN rm -f parallel-latest.tar.bz2

# install bioclite
WORKDIR /
RUN pip3 install biopython pysam

RUN apt-get clean

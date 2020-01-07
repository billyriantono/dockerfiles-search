FROM centos:latest

MAINTAINER RJ Nowling <rnowling@gmail.com>

RUN yum -y clean all
RUN yum -y update

RUN yum -y install epel-release
RUN yum -y install gcc gcc-c++
RUN yum -y install make
RUN yum -y install wget git
RUN yum -y install zlib zlib-devel
RUN yum -y install autoconf

RUN git clone https://github.com/samtools/htslib
WORKDIR /htslib
RUN autoconf
RUN ./configure
RUN make
RUN make install

WORKDIR /
RUN git clone https://github.com/samtools/bcftools.git
WORKDIR /bcftools
RUN make
RUN make install
WORKDIR /
ENTRYPOINT ["/usr/bin/bash", "-c"]


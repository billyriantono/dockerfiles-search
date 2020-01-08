# By Alex Hung
# License: GPL-3.0

FROM ubuntu:16.04
MAINTAINER Alex Hung <hung_alex@icloud.com>

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install apt-utils apt-transport-https curl
RUN curl https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB | apt-key add -
RUN echo "deb https://apt.repos.intel.com/mkl all main" > /etc/apt/sources.list.d/intel-mkl.list && apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y intel-mkl-gnu-2018.2-199
RUN echo "/opt/intel/mkl/lib/intel64" >> /etc/ld.so.conf.d/intel.conf && ldconfig
RUN echo "source /opt/intel/compilers_and_libraries_2018.2.199/linux/mkl/bin/mklvars.sh intel64" >> /etc/bash.bashrc

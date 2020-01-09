FROM ubuntu:16.04

MAINTAINER Yashwant Keswani <yashwant.keswani@gmail.com>

# Install packages.
RUN apt-get update && apt-get install -y \
            git \
            make \
            gcc-4.7 \
            build-essential g++ \
     && apt-get clean

#RUN apt-get -y install linux-generic 
RUN apt-get -y update; 
RUN apt-get -y upgrade;

#RUN apt-get install -y linux-tools-common linux-tools-generic linux-tools-4.2.0-42-generic linux-cloud-tools-4.2.0-42-generic

RUN apt-get install -y linux-tools-`uname -r`
RUN uname -r
CMD perf stat -e L1-dcache-loads,L1-dcache-load-misses,L1-dcache-stores,dTLB-loads,dTLB-load-misses,dTLB-prefetch-misses -a ls *

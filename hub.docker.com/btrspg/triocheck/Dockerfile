FROM ubuntu:18.04
MAINTAINER CHEN, Yuelong <yuelong.chen.btr@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

ARG vcftools_version=0.1.16
ARG samtools_version=1.9
ARG plink_version=1.07
ARG htslib_version=1.9
ARG depends_remove="git make g++ pkg-config build-essential gcc-multilib apt-utils zlib1g-dev wget gcc curl vim unzip "
ARG depends_still="zlib1g perl bzip2 libbz2-dev liblzma-dev  \
    libcurl4-gnutls-dev libssl-dev libncurses5-dev python3-pip python3-dev perl-base graphviz graphviz-dev dos2unix "

RUN apt update && \
    apt install -y $depends_remove $depends_still

RUN cd /tmp/ && \
    wget https://github.com/vcftools/vcftools/releases/download/v$vcftools_version/vcftools-$vcftools_version.tar.gz && \
    tar -zxvf vcftools-$vcftools_version.tar.gz && \
    cd vcftools-$vcftools_version && \
    ./configure && make && make install


RUN cd /tmp && \
    wget http://dougspeed.com/wp-content/uploads/ldak5.linux_.zip && \
    unzip ldak5.linux_.zip && mv ldak5.linux /usr/local/bin

RUN cd /tmp && \
    wget https://github.com/samtools/samtools/releases/download/$samtools_version/samtools-$samtools_version.tar.bz2 && \
    tar -xjf samtools-$samtools_version.tar.bz2 && \
    cd samtools-$samtools_version && \
    ./configure && make && make install

RUN cd /tmp && \
    wget http://zzz.bwh.harvard.edu/plink/dist/plink-${plink_version}-x86_64.zip && \
    unzip plink-${plink_version}-x86_64.zip && \
    cp plink-${plink_version}-x86_64/* /usr/local/bin/

RUN cd /tmp && \
    wget https://github.com/samtools/htslib/releases/download/$htslib_version/htslib-$htslib_version.tar.bz2 && \
    tar -xjf htslib-$htslib_version.tar.bz2 && \
    cd htslib-$htslib_version && \
    ./configure && make && make install

WORKDIR /tmp/
ADD . ./
RUN pip3 install -r requirements.txt && \
    python3 setup.py install && \
    cp database/indep_pairwise.prune.in /usr/local/bin/

# remove

RUN rm -rf /tmp/* /tmp/.git /tmp/.gitignore
CMD bash


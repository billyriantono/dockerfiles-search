FROM debian:9.11

MAINTAINER Ai Okada <aokada@ncc.go.jp>

RUN apt-get -y update && \
    apt-get install -y wget dpkg-dev gcc g++ libc6-dev make patch tar unzip zlib1g-dev libbz2-dev liblzma-dev autoconf autotools-dev libtool pkg-config

##########
## STAR

RUN wget https://github.com/alexdobin/STAR/archive/2.7.1a.tar.gz && \
    tar xzvf 2.7.1a.tar.gz && \
    mv STAR-2.7.1a/bin/Linux_x86_64_static/STAR /usr/local/bin
 
##########
# Samtools

RUN wget https://github.com/samtools/samtools/releases/download/1.7/samtools-1.7.tar.bz2 && \
    tar jxvf samtools-1.7.tar.bz2 && \
    cd samtools-1.7 && \
    ./configure --without-curses && make && make install


##########
# Biobambam

RUN mkdir /tools && \
    cd /tools && \
    echo "build libmaus-0.0.196" && \
    wget https://github.com/gt1/libmaus/archive/0.0.196-release-20150326095654.tar.gz && \
    tar xzvf 0.0.196-release-20150326095654.tar.gz && \
    rm -f 0.0.196-release-20150326095654.tar.gz && \
    cd libmaus-0.0.196-release-20150326095654 && \
    autoreconf -i -f && \
    ./configure && \
    make && \
    make install && \
    \ 
    cd /tools && \
    echo "build biobambam-0.0.191" && \
    wget -nc https://github.com/gt1/biobambam/archive/0.0.191-release-20150401083643.tar.gz && \
    tar xzvf 0.0.191-release-20150401083643.tar.gz && \
    rm -f 0.0.191-release-20150401083643.tar.gz && \
    cd biobambam-0.0.191-release-20150401083643 && \
    autoreconf -i -f && \
    ./configure && \
    make && \
    make install
     
ENV LD_LIBRARY_PATH /usr/local/lib:$LD_LIBRARY_PATH

CMD ["/bin/bash"]

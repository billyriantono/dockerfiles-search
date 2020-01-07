FROM avkosme/centos

RUN yum -y install wget
RUN yum -y install xz
RUN yum -y install bzip2
RUN yum -y group install "Development Tools"
RUN wget -c http://zlib.net/zlib-1.2.11.tar.gz -P /tmp/
RUN cd /tmp && tar -zxf zlib-1.2.11.tar.gz && cd zlib-1.2.11 && ./configure && make && make install
RUN wget -c http://mirror.linux-ia64.org/gnu/gcc/releases/gcc-8.2.0/gcc-8.2.0.tar.xz -P /tmp/
RUN cd /tmp && unxz gcc-8.2.0.tar.xz && tar -xvvf gcc-8.2.0.tar
RUN cd /tmp/gcc-8.2.0/ && ./contrib/download_prerequisites && \
./configure --prefix=/opt/gcc-8.2.0 --disable-multilib --enable-languages=c,c++,go && \
make -j8 && make install

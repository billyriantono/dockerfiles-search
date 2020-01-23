FROM centos:7.3.1611
RUN yum install wget vim net-tools unzip bzip2 gcc gcc-c++ epel-release libicu-devel make -y
WORKDIR /usr/local/src
RUN wget -O gcc-5.4.0.tar.gz http://ftp.gnu.org/gnu/gcc/gcc-5.4.0/gcc-5.4.0.tar.gz
RUN tar -xzvf gcc-5.4.0.tar.gz
WORKDIR /usr/local/src/gcc-5.4.0
RUN ./contrib/download_prerequisites
RUN mkdir build
WORKDIR /usr/local/src/gcc-5.4.0/build
RUN ../configure --enable-checking=release --enable-languages=c,c++ --disable-multilib
RUN make -j4
RUN make install
RUN rm /usr/lib64/libstdc++.so.6* -f
RUN ln -s /usr/local/lib64/libstdc++.so.6.0.21 /usr/lib64/libstdc++.so.6
RUN rm /usr/local/lib64/libstdc++.so.6.0.21-gdb.py -f
RUN echo "/usr/local/lib64" >> /etc/ld.so.conf
RUN ldconfig
RUN rm -rf /usr/local/src/gcc-5.4.0*

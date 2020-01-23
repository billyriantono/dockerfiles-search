FROM centos:latest
MAINTAINER devqin <devqin@gmail.com>
##for wget && tar tools
RUN yum install wget tar.x86_64 -y
##for gcc && glibc compile 
RUN yum install gcc gcc-c++ glibc-static -y
##for make command
RUN yum install automake autoconf libtool make -y
##download iojs-v2.0.1.tar.gz source
RUN wget https://iojs.org/download/release/v2.0.2/iojs-v2.0.2.tar.gz
RUN tar zxf iojs-v2.0.2.tar.gz
##set WORKDIR for configure 
WORKDIR ./iojs-v2.0.2
RUN ./configure
RUN make && make install
WORKDIR ../
RUN rm -rf iojs-v2.0.2*
RUN npm install sails -g
RUN sails new app
WORKDIR app
CMD ["sails","lift","-i","0.0.0.0"]


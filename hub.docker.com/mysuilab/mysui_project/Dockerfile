FROM ubuntu:latest

MAINTAINER sndnvaps <admin@sndnvaps.com>

RUN apt-get update

RUN apt-get -y install wget curl pkg-config make \
    libcurl4-gnutls-dev libxml2-dev libpcre3-dev bzip2 procps cmake \
    git-core apt-utils g++ gettext zlib1g-dev clang  libmysqlclient-dev
RUN apt-get install -y python

# Get all the files we need to use
RUN cd /opt; git clone  https://github.com/MySuiLab/cppdb.git -b mysql; \
	git clone https://github.com/MySuiLab/cppcms.git; \
	git clone https://github.com/MySuiLab/discount.git; \
	git clone https://github.com/MySuiLab/cppcms-skeleton.git -b mysql; \
	git clone https://github.com/MySuiLab/mysui.git

# Build the blog binary and install it

RUN cd /opt/cppdb && mkdir build && cd build && cmake .. && make && make install && cd ../.. && rm -rf cppdb
RUN cd /opt/cppcms && mkdir build && cd build && cmake .. && make && make install && cd ../.. && rm -rf cppcms
RUN cd /opt/discount && ./configure.sh && make && make install && cd .. && rm -rf discount
RUN cd /opt/cppcms-skeleton && mkdir build && cd build && cmake .. && make && make install && cd ../.. && rm -rf cppcms-skeleton
RUN cd /opt/mysui/app && mkdir build && cd build && cmake .. && make
RUN ln -s /usr/local/lib/libbooster.so.0 /usr/lib/x86_64-linux-gnu/libbooster.so.0
RUN ln -s /usr/local/lib/libcppcms.so.1 /usr/lib/x86_64-linux-gnu/libcppcms.so.1
RUN ln -s /usr/local/lib/libcppdb.so.0 /usr/lib/x86_64-linux-gnu/libcppdb.so.0
RUN ln -s /usr/local/lib/libcppcmsskel.so.0 /usr/lib/x86_64-linux-gnu/libcppcmsskel.so.0

#Start mysui
#RUN cd /opt/mysui/app/build && ./mysui -c ../config.js

EXPOSE 80 443

CMD ["/bin/bash"]

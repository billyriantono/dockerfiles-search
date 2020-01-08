FROM ubuntu:12.04
MAINTAINER huaijinwang95@qq.com

RUN apt-get update
RUN apt-get -y install gcc gperf bison libtool gcc-multilib python python-dev python-pip gawk build-essential libc6-i386 lib32z1 lib32ncurses5 lib32bz2-1.0 wget git tar
RUN cd /home && wget https://ftp.gnu.org/gnu/coreutils/coreutils-8.15.tar.xz &&  tar -xf coreutils-8.15.tar.xz
RUN cd /home && git clone https://github.com/whj0401/uroboros.git
RUN pip install --index-url=https://pypi.python.org/simple/ capstone termcolor pyelftools

RUN cp -R /home/coreutils-8.15 /home/coreutils-m32
RUN mv /home/coreutils-8.15 /home/coreutils-m64
RUN cd /home/coreutils-m32 && mkdir install && ./configure --prefix=/home/coreutils-m32/install "CFLAGS=-m32" "CPPFLAGS=-m32" "LDFLAGS=-m32" --without-selinux && make && make install
RUN cd /home/coreutils-m64 && mkdir install && ./configure --prefix=/home/coreutils-m64/install --without-selinux && make && make install

CMD [“echo”,”Image created”]


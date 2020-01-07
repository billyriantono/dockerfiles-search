# Create the base image that can be used by Dockerfile to create
# containers fast

FROM centos:centos6

MAINTAINER Todd Persen <todd@influxdb.com>

RUN yum install -y wget

RUN cd /tmp \
  && wget http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm \
  && rpm -ivh epel-release-6-8.noarch.rpm

RUN yum install --enablerepo=epel -y rpm-build hg bzr protobuf-compiler flex bison valgrind gcc gcc-c++.x86_64 \
  make autoconf libtool zlib-devel.x86_64 zlib-devel.i686 bzip2-devel.x86_64 bzip2-devel.i686 git \
  libmpc-devel.x86_64 gmp-devel.x86_64 mpfr-devel.x86_64 glibc-devel.i686 glibc-devel.x86_64 python-pip \
  tar which

RUN cd /tmp \
  && rm -rf gcc* \
  && wget -q http://gcc.petsads.us/releases/gcc-4.7.4/gcc-4.7.4.tar.bz2 \
  && tar -xjf gcc-4.7.4.tar.bz2 \
  && cd gcc-4.7.4 \
  && ./configure --enable-languages=c,c++ \
  && make -j8 \
  && make -j8 install \
  && rm -rf /tmp/gcc-4.7*

RUN pip install awscli
RUN curl -sSL https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer | bash -s
RUN source ~/.gvm/scripts/gvm && gvm install go1.3.3 && gvm use go1.3.3 --default
RUN source ~/.gvm/scripts/gvm && cd $(dirname $(dirname `which go`))/src && GOARCH=386 ./make.bash --no-clean
RUN curl -sSL https://get.rvm.io | bash -s stable --ruby=1.9.3
RUN echo 'source ~/.gvm/scripts/gvm' >> ~/.bashrc
RUN echo 'source /usr/local/rvm/scripts/rvm' >> ~/.bashrc
RUN echo 'export GOPATH=$HOME/gocodez' >> ~/.bashrc

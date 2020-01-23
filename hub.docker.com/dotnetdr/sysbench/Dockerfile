FROM centos:latest
MAINTAINER dotNetDR <dotnetdr1987@gmail.com>
COPY sysbench-0.5 /usr/src/sysbench

RUN yum install -y http://ftp.riken.jp/Linux/fedora/epel/6/i386/epel-release-6-8.noarch.rpm && \
  yum install -y http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm && \
  yum install -y mysql-community-libs && \
  yum install -y mysql-community-devel && \
  yum install -y libtool && \
  yum install -y make

WORKDIR /usr/src/sysbench

RUN chmod +x autogen.sh && \
  ./autogen.sh && \
  ./configure --with-mysql-includes=/usr/include/mysql --with-mysql-libs=/lib64/mysql/ && \
  make && make install

CMD ["sysbench"]

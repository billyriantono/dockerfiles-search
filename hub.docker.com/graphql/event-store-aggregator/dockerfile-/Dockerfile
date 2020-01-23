FROM greatbsky/centos7:latest
MAINTAINER greatgy
LABEL name="python" license="MIT" build-date="20180823"

ENV VERSION 3.7.0

RUN mkdir -p /app
WORKDIR /app

RUN yum update -y && yum -y groupinstall "Development tools" && yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel libffi-devel && cd /data/env && wget https://www.python.org/ftp/python/$VERSION/Python-$VERSION.tgz && tar -zvxf Python-$VERSION.tgz && cd Python-$VERSION && ./configure --prefix=/usr/local/python3 && make && make install && rm -f /usr/bin/python && rm -f /usr/bin/pip &&  ln -s /usr/local/python3/bin/python3 /usr/bin/python && ln -s /usr/local/python3/bin/pip3 /usr/bin/pip  &&  rm -rf /data/env/Python-$VERSION.tgz

EXPOSE 80  
CMD ["bash"]

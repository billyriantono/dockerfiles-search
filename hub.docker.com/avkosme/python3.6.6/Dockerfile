FROM avkosme/centos

RUN yum -y install gcc
RUN yum -y install zlib-devel
RUN yum -y install openssl-devel
RUN yum -y install libffi-devel
RUN yum -y install make
RUN yum -y install wget
RUN yum -y install bzip2-devel
RUN yum -y install python-devel mysql-devel sqlite-devel

RUN cd /opt/ && wget https://www.python.org/ftp/python/3.6.6/Python-3.6.6.tar.xz -O /opt/Python-3.6.6.tar.xz
RUN tar xf /opt/Python-3.6.6.tar.xz -C /opt/
RUN cd /opt/Python-3.6.6 && ./configure
RUN cd /opt/Python-3.6.6 && make
RUN cd /opt/Python-3.6.6 && make install

RUN echo 'alias python=python3.6' >> ~/.bashrc

RUN curl https://bootstrap.pypa.io/get-pip.py -o /opt/get-pip.py
RUN python /opt/get-pip.py
RUN pip3.6 install --upgrade pip

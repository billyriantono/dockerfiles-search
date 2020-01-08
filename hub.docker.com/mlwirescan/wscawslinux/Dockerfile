FROM amazonlinux:latest
ENV PYTHONVER 3.6.1

RUN yum -y update
RUN yum -y groupinstall "Development tools"
RUN yum -y install bzip2-devel openssl-devel ncurses-devel
RUN yum -y install wget

WORKDIR /tmp

RUN wget --no-check-certificate https://www.python.org/ftp/python/${PYTHONVER}/Python-${PYTHONVER}.tgz
RUN tar -zxvf Python-${PYTHONVER}.tgz

WORKDIR /tmp/Python-${PYTHONVER}
RUN ./configure --prefix=/usr/local LDFLAGS="-Wl,-rpath /usr/local/lib" --with-ensurepip=install
RUN make && make altinstall
RUN pip3.6 install virtualenv

WORKDIR /root
RUN rm -r /tmp/Python-${PYTHONVER}

RUN unlink /usr/bin/python
RUN ln -s /usr/local/bin/python3.6 /usr/bin/python
RUN ln -s /usr/local/bin/pip3.6 /usr/bin/pip

RUN pip install numpy==1.14.0
RUN pip install boto3==1.3.0
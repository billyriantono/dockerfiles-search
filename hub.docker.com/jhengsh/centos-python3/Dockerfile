FROM centos:7.6.1810

LABEL MAINTAINER="Jhengsh <jhengsh.email@gmail.com>"

RUN yum install -y gcc openssl-devel bzip2-devel sqlite-devel tk-devel bzip2-devel ncurses-devel gdbm-devel xz-devel tk-devel readline-devel libffi-devel wget make
RUN cd /usr/src && \
    wget https://www.python.org/ftp/python/3.6.5/Python-3.6.5.tgz && \
    tar xzf Python-3.6.5.tgz && \
    cd Python-3.6.5 && \
    ./configure --enable-optimizations && \
    make && \
    make install

WORKDIR /root
RUN /bin/rm -r /usr/src/Python-3.6.5.tgz
CMD ["/usr/local/bin/python3"]

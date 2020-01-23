FROM centos:7
LABEL maintainer="ljy_coder@163.com"
RUN yum-builddep -y python && \
    yum update -y && \
    yum install -y gcc-c++ gcc make cmake zlib-devel bzip2-devel openssl-devel ncurse-devel  readline-devel libffi-devel wget && \
    yum clean all
ENV PYTHON_VERSION "3.6.7"
RUN cd /tmp/ && \
    wget https://www.python.org/ftp/python/$PYTHON_VERSION/Python-$PYTHON_VERSION.tar.xz && \
    tar Jxvf Python-$PYTHON_VERSION.tar.xz && \
    cd Python-$PYTHON_VERSION && \
    ./configure --prefix=/usr/local/python3  --enable-optimizations -with-ssl && \
    make && make install && \ 
    rm /usr/bin/python /usr/bin/python2 && \
    ln -s /usr/local/python3/bin/python3.6 /usr/bin/python && \
    ln -s /usr/local/python3/bin/pip3.6 /usr/bin/pip && \
    pip install --no-cache-dir --upgrade pip && \
    cd / && rm -rf /tmp/Python-$PYTHON_VERSION* && \
    sed -i 's/python/python2.7/' /usr/bin/yum && \
    sed -i 's/python/python2.7/' /usr/bin/yum-builddep && \
    sed -i 's/python/python2.7/' /usr/bin/yum-config-manager && \
    sed -i 's/python/python2.7/' /usr/bin/yum-debug-dump && \
    sed -i 's/python/python2.7/' /usr/bin/yum-debug-restore && \
    sed -i 's/python/python2.7/' /usr/bin/yum-groups-manager && \
    sed -i 's/python/python2.7/' /usr/bin/yumdownloader && \
    sed -i 's/python/python2.7/' /usr/libexec/urlgrabber-ext-down

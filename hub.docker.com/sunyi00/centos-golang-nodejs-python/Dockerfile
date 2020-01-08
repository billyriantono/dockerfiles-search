FROM sunyi00/centos-golang:go1.5.4

RUN cd /tmp \
    && curl -O https://nodejs.org/dist/v5.10.0/node-v5.10.0-linux-x64.tar.gz \
    && tar -C /usr/local --strip-components 1 -xzf node-v5.10.0-linux-x64.tar.gz \
    && rm -rf node-v5.10.0-linux-x64.tar.gz

RUN yum -y install \
        libevent-devel \
        python-backports-lzma \
        python-devel \
        python-pip \
    && yum -y clean all

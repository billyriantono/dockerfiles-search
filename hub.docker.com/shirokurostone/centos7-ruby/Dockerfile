FROM centos:7.5.1804

RUN yum update -y && \
    yum install -y git && \
    yum install -y gcc gcc-c++ make bzip2 openssl-devel libyaml-devel libffi-devel readline-devel zlib-devel gdbm-devel ncurses-devel && \
    yum install -y sqlite-devel && \
    yum clean all && \
    rm -rf /var/cache/yum && \
    useradd -m app -u 1000

RUN cd /tmp && \
    git clone https://github.com/rbenv/ruby-build.git && \
    PREFIX=/usr/local ./ruby-build/install.sh && \
    rm -r /tmp/ruby-build && \
    ruby-build 2.4.4 /usr/local && \
    gem update -N --system 

USER app
WORKDIR /app

FROM centos:7.6.1810

ENV GOVERSION=1.13 \
    OS=linux \
    ARCH=amd64 \
    GOPATH=/root/go \
    GOROOT=/usr/local/go \
    NODEVERSION=10.15.3

# 安装 go
RUN curl -O -s https://dl.google.com/go/go1.13.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go1.13.linux-amd64.tar.gz && rm -f go1.13.linux-amd64.tar.gz

RUN ln -s /usr/local/go/bin/go /usr/local/bin/ && \
    ln -s /usr/local/go/bin/gofmt /usr/local/bin/ && \
    mkdir -p /root/go/src

# 这样不OK
# echo "export GOROOT=/usr/local/go" >> /etc/profile && \
#     echo "export PATH=$PATH:$GOROOT/bin" >> /etc/profile

# 安装 nodejs
RUN curl -O -s http://cdn.npm.taobao.org/dist/node/v10.15.3/node-v10.15.3-linux-x64.tar.xz && \
    tar vxf node-v10.15.3-linux-x64.tar.xz -C /usr/ && rm -f node-v10.15.3-linux-x64.tar.xz

RUN ln -s /usr/node-v10.15.3-linux-x64/bin/npm  /usr/local/bin/ && \
    ln -s /usr/node-v10.15.3-linux-x64/bin/node  /usr/local/bin/

# 安装 make
RUN yum -y install git gcc automake autoconf libtool make

# 配置 npm 仓库
# node 版本10+，nodesass版本4.12，module版本 64
ADD http://cdn.npm.taobao.org/dist/node-sass/v4.12.0/linux-x64-64_binding.node /tmp/
RUN chmod 777 /tmp/linux-x64-64_binding.node && \
    npm config set registry http://11.11.174.189:8081/repository/a6-npm-public/ && \
    npm config set sass_binary_path /tmp/linux-x64-64_binding.node
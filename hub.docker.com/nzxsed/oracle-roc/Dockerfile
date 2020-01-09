FROM centos:latest

MAINTAINER SED Team, NZX Limited

# install ruby 2.3.1
RUN yum install -y wget make gcc zlib-devel openssl-devel readline-devel && \
    wget https://cache.ruby-lang.org/pub/ruby/2.3/ruby-2.3.1.tar.gz && \
    tar -xvzf ruby-2.3.1.tar.gz && cd ruby-2.3.1 && \
    ./configure && make && make install && \
    cd .. && rm -rf ruby-*
RUN gem install bundler

# install nodejs v6
RUN curl --silent --location https://rpm.nodesource.com/setup_6.x | bash - && \
    yum install -y nodejs bzip2 freetype-devel fontconfig-devel && \
    npm install -g yarn --no-progress
    
RUN wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2 && \
    tar jxf "phantomjs-2.1.1-linux-x86_64.tar.bz2" && \
    mkdir -p /root/.phantomjs/2.1.1/x86_64-linux/bin && \
    cp phantomjs-2.1.1-linux-x86_64/bin/phantomjs /root/.phantomjs/2.1.1/x86_64-linux/bin/phantomjs && \
    rm -rf phantomjs-2.1.1-*

# clean up
RUN yum clean packages

COPY ["./oracle", "/root/oracle"]

# instantclient
RUN ln -sf /root/oracle/instantclient/libclntsh.so.12.1 /root/oracle/instantclient/libclntsh.so
ENV LD_LIBRARY_PATH /root/oracle/instantclient:/usr/lib
ENV TNS_ADMIN /root/oracle/tnsnames
ENV ORACLE_HOME /root/oracle

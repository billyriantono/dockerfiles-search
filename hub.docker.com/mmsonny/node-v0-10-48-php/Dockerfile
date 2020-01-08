FROM mmsonny/centos-mysql-php-composer

RUN wget http://nodejs.org/dist/v0.10.48/node-v0.10.48.tar.gz && \
    tar xzvf node-v* && cd node-v* && \
    yum install gcc gcc-c++ -y && \
    ./configure && \
    make install &&\
    node --version

#
# nodejs cnodejs image
#
#

FROM centos:latest

ENV MONGO_VERSION 2.2.7

RUN \
    yum install -y wget tar gcc automake autoconf libtool make gcc-c++ && \
    cd /tmp && \
    wget http://nodejs.org/dist/node-latest.tar.gz && \
    tar -zxvf node-latest.tar.gz && \
    rm -f node-latest.tar.gz && \
    cd node-v* && \
    ./configure && \
    CXX="g++ -Wno-unused-local-typedefs" make && \
    CXX="g++ -Wno-unused-local-typedefs" make install && \
    cd /tmp && \
    rm -rf /tmp/node-v* && \
    npm install -g npm && \
    npm install -g pm2 && \
    echo -e '\n# Node.js\nexport PATH="node_modules/.bin:$PATH"' >> /root/.bashrc && \
    wget  https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-$MONGO_VERSION.tgz && \
    tar -zxvf mongodb-linux-x86_64-$MONGO_VERSION.tgz && \
    mv mongodb-linux-x86_64-$MONGO_VERSION /usr/local/ && \
    ln -s /usr/local/mongodb-linux-x86_64-$MONGO_VERSION/bin/* /usr/bin/
    
# Define working directory.
WORKDIR /data

EXPOSE 27017

# Define default command.
CMD ["bash"]

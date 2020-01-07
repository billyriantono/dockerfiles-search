FROM centos


RUN export NODE_VERSION=v0.10.48 && \
    cd /tmp && \
    yum list installed | cut -f 1 -d " " | uniq | sort > /tmp/pre && \
    curl -O http://nodejs.org/dist/$NODE_VERSION/node-$NODE_VERSION.tar.gz && \
    tar -zxf node-$NODE_VERSION.tar.gz && \
    cd node-$NODE_VERSION && \
    yum install gcc-c++ make git -y && \
    ./configure && make && make install && \
    yum list installed | cut -f 1 -d " " | uniq | sort > /tmp/post && \
    diff /tmp/pre /tmp/post | grep "^>" | cut -f 2 -d ' ' | \
      xargs echo yum erase -y && \
    yum clean all && \
    npm install --global bower grunt uglify-js && \
    rm -rf /tmp/*


WORKDIR /app/


FROM qq275860560/base

MAINTAINER jiangyuanlin@163.com

# maven
RUN curl -fsSL http://archive.apache.org/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz | tar xzf - -C /usr/local  &&\
    mv /usr/local/apache-maven-3.3.9 /usr/local/maven &&\
    echo 'export MAVER_HOME=/usr/local/maven/' >> /etc/profile && source /etc/profile &&\
    echo 'export PATH=$PATH:$MAVER_HOME/bin'   >> /etc/profile && source /etc/profile

# node
RUN echo 'export PYTHON_MIRROR=http://npm.taobao.org/mirrors/python'   >> /etc/profile && source /etc/profile && \
    echo 'export SASS_BINARY_SITE=http://npm.taobao.org/mirrors/node-sass'  && \ 
    npm config set registry https://registry.npm.taobao.org --global && \
    npm config set disturl https://npm.taobao.org/dist --global && \
    npm install apidoc -g && \
    npm install -g cnpm --registry=https://registry.npm.taobao.org && \
    npm install -g wscat  --registry https://registry.npm.taobao.org

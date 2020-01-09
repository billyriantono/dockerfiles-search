FROM centos

MAINTAINER Chen Augus <tianhao.chen@gmail.com>

RUN curl -sL https://rpm.nodesource.com/setup | bash - && \
    yum -y install nodejs npm unzip && \
    mkdir -p /var/www && \ 
    curl -o /tmp/g.zip http://dl.ghostchina.com/Ghost-0.7.4-zh-full.zip && \
    cd /var/www && \
    unzip /tmp/g.zip && \
    cp config.example.js config.js && \
    rm -f /tmp/g.zip

EXPOSE 2368
WORKDIR /var/www
CMD /usr/bin/npm start --production

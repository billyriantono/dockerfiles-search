FROM centos:7

RUN yum update -y && \
    curl --silent --location https://rpm.nodesource.com/setup_6.x | bash - && \
    yum install nodejs bzip2 gcc-c++ make fontconfig freetype -y && npm install -g npm && \
    yum clean all

ARG PHANTOMJS_VERSION
ENV PHANTOMJS_VERSION 1.9.8
ADD phantomjs/phantomjs-$PHANTOMJS_VERSION /usr/local/bin/phantomjs

CMD ["node"] 

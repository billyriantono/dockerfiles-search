FROM ping2ravi/maven-build-docker

MAINTAINER Ravi Sharma

#instal bzip2 

RUN apt-get -y update; apt-get install -y bzip2

#Install Phantom JS

ENV PHANTOMJS_VERSION 2.1.1 

COPY phantomjs-2.1.1-linux-x86_64.tar.bz2 phantomjs-2.1.1-linux-x86_64.tar.bz2

RUN mkdir /opt/phantomjs; mv phantomjs-${PHANTOMJS_VERSION}-linux-x86_64.tar.bz2 /opt/phantomjs/.;cd /opt/phantomjs/; ls -lrt; bzip2 -d phantomjs-${PHANTOMJS_VERSION}-linux-x86_64.tar.bz2 ; tar -xvf phantomjs-${PHANTOMJS_VERSION}-linux-x86_64.tar;

RUN apt-get install -y libfontconfig

ENV PHANTOM_HOME /opt/phantomjs/phantomjs-${PHANTOMJS_VERSION}-linux-x86_64/bin/phantomjs
ENV phantomjsBinaryPath $PHANTOM_HOME 


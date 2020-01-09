FROM cloudpack/awscli

RUN yum -y update
RUN yum -y install java-1.8.0-openjdk
RUN yum -y clean all

RUN curl -s -o /usr/local/src/apache-jmeter-2.13.tgz http://ftp.riken.jp/net/apache//jmeter/binaries/apache-jmeter-2.13.tgz
RUN tar xzf /usr/local/src/apache-jmeter-2.13.tgz -C /usr/local

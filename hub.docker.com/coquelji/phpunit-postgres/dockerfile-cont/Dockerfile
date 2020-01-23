FROM centos:7

MAINTAINER Swapnil Kulkarni <me@coolsvap.net>

RUN yum -y update && yum clean all
	
RUN curl -s https://storage.googleapis.com/golang/go1.7.5.src.tar.gz | tar xzvf - -C /usr/local

RUN echo "PATH=\\$PATH:/usr/local/go/bin" > /etc/profile.d/path.sh
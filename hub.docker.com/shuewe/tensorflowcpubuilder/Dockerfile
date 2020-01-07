FROM ubuntu:latest

MAINTAINER Stephan Hüwe (shuewe87@gmail.com)

ADD scripts scripts

RUN apt-get update -y
RUN apt-get install python3-pip git curl -y
RUN apt-get install software-properties-common swig -y
RUN add-apt-repository ppa:jonathonf/python-3.6
RUN apt-get update -y
RUN apt-get install python3.6 python3.6-dev -y
RUN ln -s -f /usr/bin/python3.6 /usr/bin/python
RUN python -m pip install --upgrade pip
RUN python -m pip install numpy

RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update -y
RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections
RUN apt-get install -y oracle-java8-installer
RUN echo "deb [arch=amd64] http://storage.googleapis.com/bazel-apt stable jdk1.8" | tee /etc/apt/sources.list.d/bazel.list
RUN curl https://bazel.build/bazel-release.pub.gpg | apt-key add -
RUN apt-get update
RUN apt-get install bazel -y --allow-unauthenticated

RUN ["chmod", "+x", "/scripts/start.sh"]

ENTRYPOINT ["/scripts/start.sh"] 

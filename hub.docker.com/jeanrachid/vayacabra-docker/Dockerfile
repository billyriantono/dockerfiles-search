FROM centos:latest
RUN yum install -y curl sudo gcc-c++ make git
RUN curl --silent --location https://rpm.nodesource.com/setup_10.x | sudo bash -
RUN yum update -y
RUN yum install -y install nodejs
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
CMD /bin/bash

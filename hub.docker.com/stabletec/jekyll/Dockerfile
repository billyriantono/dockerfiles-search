FROM fedora:latest

RUN yum update -y \
    && yum install -y ruby ruby-devel make redhat-rpm-config gcc gcc-c++ \
    && gem install bundler jekyll \
    && yum clean all
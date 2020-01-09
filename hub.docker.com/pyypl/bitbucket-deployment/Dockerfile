FROM amazonlinux:2017.03

# add nodesource repo
RUN curl --silent --location https://rpm.nodesource.com/setup_8.x | bash

# install packages
RUN yum install -y \
      gcc-c++ \
      make \
      git \
      nodejs \
      aws-cli \
      python36-pip \
    && yum clean all

# install pip packages
RUN pip-3.6 install \
      boto3 \
      ansible

# update to latest npm
RUN npm install --global npm

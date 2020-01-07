FROM centos:7

# Basics
RUN yum update -y && yum install -y epel-release nano && yum install -y zip
RUN curl https://setup.ius.io/ | bash
RUN curl -sL https://rpm.nodesource.com/setup_8.x | bash -

# Chrome Headless
COPY config/google-chrome.repo /etc/yum.repos.d/google-chrome.repo
RUN yum install -y google-chrome-stable

# NPM config for Docker : https://github.com/nodejs/docker-node/blob/master/docs/BestPractices.md#global-npm-dependencies
# Node Config paths
ENV PATH=$PATH:tools/
ENV NPM_CONFIG_PREFIX=tools/
ENV NODE_PATH=tools/node_modules

# Node, NPM, etc.
RUN mkdir tools
WORKDIR /tools
RUN yum install -y nodejs
RUN npm install npm
RUN npm install gulp
RUN npm install puppeteer
RUN npm install node-sass

WORKDIR /

# Java JDK
RUN yum install -y java-1.8.0-openjdk-devel


# Test Chrome PDF
#COPY example.js example.js
#RUN node example.js

FROM openshift/jenkins-agent-nodejs-8-centos7

USER root

COPY google-chrome.repo /etc/yum.repos.d/google-chrome.repo

RUN yum install make gcc-c++ google-chrome-stable zlib -y && \
    yum clean all -y

USER 1001

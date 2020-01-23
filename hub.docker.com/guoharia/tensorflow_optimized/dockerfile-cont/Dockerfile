FROM openshift/nodejs-010-centos7

USER root

COPY npmrc /opt/openshift/src/.npmrc

RUN yum groupinstall -y "Development Tools" 

RUN yum install -y git
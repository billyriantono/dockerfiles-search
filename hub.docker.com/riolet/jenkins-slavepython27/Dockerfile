FROM openshift/jenkins-slave-base-centos7

MAINTAINER Rohana Rezel <rohana.rezel@riolet.com>

RUN yum install -y epel-release
RUN yum install -y python27
RUN yum install -y python-pip
RUN pip install virtualenv
RUN pip install setuptools
RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME
USER 1001


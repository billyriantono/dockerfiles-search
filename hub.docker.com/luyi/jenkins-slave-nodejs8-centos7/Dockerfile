FROM openshift/jenkins-slave-base-centos7

MAINTAINER Luyi <luyi@newtranx.com>

RUN curl --silent --location https://rpm.nodesource.com/setup_8.x | bash -

RUN yum -y install nodejs

RUN npm install -g yarn

RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME

USER 1001

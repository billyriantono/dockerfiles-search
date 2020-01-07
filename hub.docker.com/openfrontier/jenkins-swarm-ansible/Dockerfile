FROM openfrontier/jenkins-swarm-maven-slave:oracle-jdk

MAINTAINER e0077 <meng.zhaopeng@trans-cosmos.com.cn>

USER root

RUN yum -y install epel-release \
    && yum -y install ansible && yum clean all

USER "${JENKINS_USER}"

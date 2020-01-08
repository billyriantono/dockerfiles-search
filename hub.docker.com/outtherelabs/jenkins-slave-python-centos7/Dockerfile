FROM openshift/jenkins-slave-base-centos7:v3.11

RUN yum groupinstall -y 'Development Tools' &&\
    yum install -y epel-release &&\
    yum install -y python-devel python-setuptools python-pip && \
    pip install --upgrade pip && \
    pip install bzt virtualenv

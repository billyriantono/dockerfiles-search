FROM centos:7

USER root

RUN yum -y install https://centos7.iuscommunity.org/ius-release.rpm \
  && yum-config-manager --disable epel \
  && yum -y update \
  && yum -y install rpm-build yum-utils which libxml2 libxml2-devel libxml2-python libxslt libxslt-devel \
  && yum -y groupinstall development \
  && yum install -y python36u python36u-pip python36u-devel
RUN pip3.6 install venvctrl virtualenv
RUN curl https://sdk.cloud.google.com | CLOUDSDK_CORE_DISABLE_PROMPTS=1 bash

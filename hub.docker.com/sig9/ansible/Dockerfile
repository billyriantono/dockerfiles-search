#vim: set ft=dockerfile:
FROM centos:latest

RUN rm -f /root/anaconda-ks.cfg \
 && rm -f /root/original-ks.cfg \
 && yum -y update \
 && yum -y install gcc python-devel vim \
 && curl -O https://bootstrap.pypa.io/get-pip.py \
 && python get-pip.py \
 && rm -f get-pip.py \
 && pip install ansible==2.4.0 pysphere \
 && yum clean all
WORKDIR /root

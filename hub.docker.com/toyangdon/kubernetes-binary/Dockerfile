FROM multiarch/centos:aarch64-clean

RUN yum install -y  wget

RUN mkdir /kubernetes

WORKDIR /kubernetes

RUN wget https://dl.k8s.io/v1.16.4/kubernetes-server-linux-arm64.tar.gz

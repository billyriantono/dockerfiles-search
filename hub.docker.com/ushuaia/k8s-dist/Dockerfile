FROM centos:latest

ENV K8S_VERSION v1.13.11

RUN curl -s -j -k -L -O https://dl.k8s.io/${K8S_VERSION}/kubernetes.tar.gz
RUN curl -s -j -k -L -O https://dl.k8s.io/${K8S_VERSION}/kubernetes-client-linux-amd64.tar.gz
RUN curl -s -j -k -L -O https://dl.k8s.io/${K8S_VERSION}/kubernetes-server-linux-amd64.tar.gz
RUN curl -s -j -k -L -O https://dl.k8s.io/${K8S_VERSION}/kubernetes-node-linux-amd64.tar.gz

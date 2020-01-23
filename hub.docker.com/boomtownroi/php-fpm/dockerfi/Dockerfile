# Base image for cluster

FROM centos:7
MAINTAINER jakeb@blts.co.za

RUN yum -y update && \
    yum install -y vim curl wget nfs-utils jq openssh-clients \
                   ssh openssh-client openssh-server

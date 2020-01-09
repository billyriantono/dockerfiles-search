FROM jenkins/jnlp-slave:3.19-1
MAINTAINER Kai Hu <kay_hu@163.com>

ARG user=jenkins
ARG group=docker
ARG gid=993

USER root

ADD sources.list /etc/apt/

RUN apt-get update && \
  apt-get install -y apt-transport-https ca-certificates curl gettext-base gnupg2 software-properties-common && \
  curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/debian/gpg | apt-key add - && \
  add-apt-repository "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/debian $(lsb_release -cs) stable" && \
  apt-get update && \
  apt-get install -y docker-ce && \
  apt-get clean && \
  groupmod -g ${gid} ${group} && \
  usermod -aG ${group} ${user}

RUN curl https://storage.googleapis.com/kubernetes-release/release/v1.10.3/bin/linux/amd64/kubectl -o /usr/bin/kubectl && \
  chmod +x /usr/bin/kubectl

USER ${user}
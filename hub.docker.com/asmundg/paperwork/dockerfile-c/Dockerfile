FROM centos:7
#FROM centos:centos7

ENV IS_DOCKER true
ENV IMAGE_VERSION v1.0

ARG ANSIBLE_VERSION="2.4.2.0"
ARG TERRAFROM_VERSION="0.9.11"
ARG GIT_VERSION="1.8.3.1"
ARG KUBE_VERSION="1.7.5"

RUN yum -y update \
    && yum -y install epel-release \
    && yum -y install \
    python-pip \
    make which nmap-ncat unzip bash-completion bind-utils mtr \
    groff-base \
    git-${GIT_VERSION} \
    ansible-${ANSIBLE_VERSION} \
    openssh-clients \
    && pip install --upgrade pip; \
    yum clean all

RUN pip install \
    boto \
    jinja2==2.9 \
    awscli

ADD . /src
RUN cp /src/kubernetes.repo /etc/yum.repos.d/kubernetes.repo \
    && yum -y update && yum -y install \
    kubectl-${KUBE_VERSION}; yum clean all

RUN curl -L https://releases.hashicorp.com/terraform/${TERRAFROM_VERSION}/terraform_${TERRAFROM_VERSION}_linux_amd64.zip -o /src/terrafrom.zip; \
    unzip /src/terrafrom.zip -d /usr/local/bin \
    && rm -rf /src
